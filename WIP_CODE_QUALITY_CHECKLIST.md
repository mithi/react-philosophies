🚧 🚧 🚧 This article is a WORK IN PROGRESS (DRAFT) 🚧 🚧 🚧 

# REACT CODE QUALITY CHECK LIST (WIP / DRAFT)

I noticed that I keep writing the same review comments over  and over again for the last 3 months so I'm writing down this check list. 

I'm going to add this as our default pull request template. 
Comments, questions, violent reactions? Please let me know.
Please populate this checklist before asking for a review. I will add more as I encounter and/or remember them.

If you find your PR to have so many requested changes, 
It's best to reread this article again: https://github.com/mithi/react-philosophies
Let's not waste each others time. Thanks!

--------------
BASIC STUFF
--------------
- [ ] Write down the summary of the changes done
- [ ] Add as many screenshots for new features
- [ ] If this is a bug, write down the problem, the cause of the issue, and the solution
- [ ] Remove console logs and commented out console logs
- [ ] Check for spelling errors
- [ ] use classNames if possible and not style, ie `className="relative mt-0"` vs `style: {{ position: "relative", marginTop: 0}}`
- [ ] If you are doing something hacky, please add a comment explaining why you did what you did. Normally, I prescribe against comments, but we should add comments on complicated code that's not easy to understand, explain why we need this code, its purpose, what it trying to accomplish. Also, if this is a temporary fix that is not-ideal and should be revisited in another time, add a comment as well. If you are using `any` as a type, please add a comment explaining why this is absolutely necessary to do.
- [ ] Never declare stuff inside your component that is not dependent on the state or props of that component, remember that react recreates the functions you declare inside the component every time it re-renders. Not only is it more performant, it's clearer as well.


--------------
KEEP THINGS SMALL AND SIMPLE
--------------
- [ ] Check if your component is doing too many things. If so, break them down by responsibilities. Refactoring is not just about reducing the lines of code for each component, it's about making components more loosely coupled (https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o),... separating concerns and responsibilities 
- [ ] Check if you are doing complicated logic and think of ways to simplify it. If you have simplified algebraic expressions in highschool, this is 10x easier. https://refactoring.guru/refactoring/techniques/simplifying-conditional-expressions
- [ ] Avoid redundant states and props  
- [ ] Avoid prop drilling by using composition https://reactjs.org/docs/composition-vs-inheritance.html
- [ ] Avoid adding new props to existing components or types unless really needed, make types cohesive
- [ ] Please do dependency injection, only pass what you need to the component. don't pass more than you need to.


--------------
NO REACTJS VIOLATIONS
--------------

- [ ] Make sure you're not violating any rule of hooks https://reactjs.org/docs/hooks-rules.html
- [ ] Make sure you're adding react keys when creating an array of components https://beta.reactjs.org/learn/rendering-lists , https://epicreact.dev/why-react-needs-a-key-prop
- [ ] Don't omit functions from a list of dependencies https://reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies , https://overreacted.io/a-complete-guide-to-useeffect/
- [ ] Check if you really need to use a `useEffect` or if it should be on an event handler instead https://beta.reactjs.org/learn/separating-events-from-effects , https://epicreact.dev/myths-about-useeffect

--------------
STYLE GUIDE
--------------

- [ ] Avoid traditional for - loops. Use `.map()` , `.filter()` etc
- [ ] Do not use switch statements, prefer early if returns https://softwareengineering.stackexchange.com/questions/206816/clarification-of-avoid-if-else-advice 
- [ ] Prefer nested ternaries when the logic is simple and easy to follow, https://medium.com/javascript-scene/nested-ternaries-are-great-361bddd0f340
- [ ] Prefer not to use nested ternaries when conditionally rendering components IE avoid logic like `shouldRender ? <BigComponent /> : <AnotherBigComponent />`, why? Completely messes up the formating
- [ ] Avoid adding helper functions inside a component, prefer to inline it, especially if that helper function is being used on two places. 
- [ ] If helper function is really needed for abstraction purposes, prefer to declare the helper function outside of the component, remember that react recreates the functions you declare inside the component everytime it rerenders 

--------------
CHECK FOR EASY TO CATCH CODE SMELLS 
--------------
- [ ] :x: Avoid Methods or functions defined with a large number of arguments
- [ ] :x: Avoid Boolean logic that may be hard to understand
- [ ] :x: Avoid Duplicate code which is syntactically identical (but may be formatted differently)
- [ ] :x: Avoid Functions or methods that may be hard to understand
- [ ] :x: Avoid Components defined with a large number of functions or methods
- [ ] :x: Avoid Excessive lines of code within a single function or method
- [ ] :x: Avoid Functions or methods with a large number of return statements
- [ ] :x: Avoid Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)

Keep in mind that code smells don't necessarily mean that code should be changed. A code smell just informs you that you might be able to think of a better way to implement the same functionality.


--------------
CONCRETE EXAMPLES
--------------


### Example 0 
:x: remember that react recreates the functions you declare inside the component everytime it rerenders 

```jsx
const MyComponent = () => {
	
  const saysHello = () => { console.log("hello") }
  return <Button onClick={saysHello} />
}
```
:white_check_mark:

```
const saysHello = () => { console.log("hello") }
 
const MyComponent = () => {	
  return <Button onClick={saysHello} />
}
```

### Example 1
 :x: Types should be cohesive
```jsx
type ItemPill = { name: string , id: string, count?: number, flowAssignmentType?: boolean, isUserItem?: boolean }
```

:white_check_mark:
```jsx
type ItemPill = { name: string , id: string, count?: number }
type UserItemPill = ItemPill & { type: "Annotator" | "Reviewer" }
```

### Example 2
 :x: Why need to pass the whole asset object when you just care about whether is it a video or not?? 
A component should just know enough to do its job and nothing more. 
```jsx
const MyComponent = ({ asset }) => {
	if(asset.metadata.type === "video") {
	  return <Video />
	}

	return  <Image />
}
```
 :white_check_mark:
```jsx
const MyComponent = ({ type }) => {
	if(type === "video") {
	  return <Video />
	}

	return <Image />
}
```
### Example 3

:x:  in this case <FacialExpression /> is responsible for: (1) displaying the emoji (2) the logic to determine what to show
```jsx
<FacialExpression hasFace={true} isHappy={true} isSecretive={false} />
```
 :white_check_mark: Separated concerns, <FacialExpression /> displays the mode, shouldShowHappyFace() determines if happy
```jsx
<FacialExpression mode={shouldDisplayHappyMode(hasFace, isHappy, isSecretive) ? "HAPPY" : "DEFAULT"} />
```
### Example 4

 :x: Avoid redundant props
```jsx
const NumberProperties = ( 
  props: {num: number, sign: "POSITIVE" | "NEGATIVE" | "ZERO", isInteger: true, isDivisibleByTwo: boolean  } 
) => {
  // displays number, sign, if integer, if divisible by two  
}
```
:white_check_mark:
```jsx
const NumberProperties = ({num} : { num: number }) => {
	const isInteger = Number.isInteger(num)
	const sign = num === 0 ? "ZERO" : num > 0 ? "POSITIVE" : "NEGATIVE"
	const isDivisibleByTwo = num % 2 === 0
	// displays number, sign, if integer, if divisible by two  
}
```
### Example 5
 :white_check_mark: no need for these single use helper function
```jsx
  private isAProjectBoard = () => {
    const url = this.state.urlPath.split("/");
    return url[3] === "project";
  };

  private isAnnotationBoard = () => {
    const url = this.state.urlPath.split("/");
    return url[3] === "annotator";
  };

  private isWorkflowBoard = () => {
    const url = this.state.urlPath.split("/");
    return url[3] === "flow";
  };

 private isShowFullBar = () => {
    return (
      this.isProjectBoard() &&
      !this.isAnnotationBoard() &&
      !this.isWorkflowBoard()
    );
  };
```
// :x: no need for these single use helper function , and reduce unnecessary recalculations
```jsx
const url = this.state.urlPath.split("/")
const isShowFullbar = ["flow", "annotator", "project"].includes(url)
```

### Example 6
:x: No need to be this verbose, nested ternaries are great especially for short conditions. see also: https://medium.com/javascript-scene/nested-ternaries-are-great-361bddd0f340
```jsx
const getClasses = () => {
    if (isProjectLoading) {
      return classes.noSideMenu;
    }

    if (isShowFullBar && isSidebarOpen) {
      return classes.sideMenuOpen;
    }
    if (isShowFullBar && !isSidebarOpen) {
      return classes.sideMenuCollapsed;
    }
    return classes.noSideMenu;
  };
```  
:white_check_mark:
```jsx
const isCollapsed = isShowFullBar && !isSidebarOpen 
const isExpanded = isShowFullBar && !isSidebarOpen 
const classes = isProjectLoading 
  ? classes.noSideMenu
  : isCollapsed
  ? classes.sideMenuCollapsed
  : isExpanded
  ? classes.sideMenuOpen
  : classes.noSideMenu
```

-----
If you find your PR to have so many requested changes, 
It's best to reread this article again: https://github.com/mithi/react-philosophies
Let's not waste each others time. Thanks!
