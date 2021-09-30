# react-philosophies

[![Epic React Exercises](https://img.shields.io/badge/Epic%20-React%20Exercises-orange.svg?logo=react&color=0abde3)](https://github.com/mithi/epic-react-exercises) [![buy me coffee](https://img.shields.io/badge/Buy%20me%20-coffee!-orange.svg?logo=buy-me-a-coffee&color=795548)](https://ko-fi.com/minimithi) [![PRs welcome!](https://img.shields.io/badge/%20📝%20Contributions-welcome-orange.svg?style=flat)](https://github.com/mithi/react-philosophies/issues) ![Forever a work in progress!](https://img.shields.io/badge/%20🚧%20Forever%20🚧%20%20-under%20construction-yellow.svg) 

If this document helped you in some way, consider [buying me a few cups of coffee ☕☕☕](https://ko-fi.com/minimithi). This motivates me to create more `React` "stuff"! 🙂 

## Table of Contents

0. [Introduction](#introduction)
1. [The Bare Minimum](#the-bare-minimum)
2. [Design for happiness](#design-for-happiness)
3. [Performance tips](#performance-tips)
4. [Testing principles](#testing-principles)

<details>
    <summary>The way this document is organized</summary>

While writing, I realized that it was actually difficult for me to separate my thoughts into the `design`, `performance`, and `testing`. A lot of designs intended for maintainability also make your application faster and easier to test. Apologies if the discussion appears to be cluttered at times. 

</details>

<details>
    <summary>Thanks to all these wonderful people for the PRs 🚜, coffee ☕, recommended readings 📚, and sharing of ideas 💡: (expand) </summary>

-----
Special thanks to the `r/reactjs` community for giving [very valuable suggestions](https://www.reddit.com/r/reactjs/comments/pvwb6m/what_i_think_about_when_i_write_code_in_react) that helped significantly improve the quality of this document.

**🚜 Pull Requests**

-  [@fengzilong](https://github.com/fengzilong)
- [@ankitwww](https://github.com/ankitwww)

**☕ Coffee!**

- Myles Banner

**📚 Readings recommended to me**

- [Out of the Tar Pit, Ben Moseley and Peter Marks (2006)](http://curtclifton.net/papers/MoseleyMarks06a.pdf), recommended by [Reddit user: icjoseph](https://www.reddit.com/u/icjoseph)

----

**💡 Comments, suggestions, violent reactions? I'd love to hear them!💡**

If there's something that you think should be part of my reading list, or if you have great ideas that you think I should include here, don't hesitate to submit a PR or an issue; I'll check it out. Any contributions to improve `react-philosophies` whether big or small are always welcome and appreciated. 

</details>


## 🧘 Introduction 

`react-philosophies` is:
- things I think about before I write `React` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve over time as my experience grows
- mostly techniques which are variations of basic [refactoring](https://en.wikipedia.org/wiki/Code_refactoring) methods, [SOLID](https://en.wikipedia.org/wiki/SOLID) principles, and [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming) ideas... just applied to `React` specifically 🙂

A lot of these things may feel like very basic and common-sense. But surprisingly, I've worked with large complex applications where these things are not taken into consideration. The examples I present here are based on code I have actually seen in production. 

`react-philosophies` is inspired by various places I've stumbled upon at different points of my coding journey.

Most notably:

- [Tim Peters: Zen of Python (Pep 20)](https://www.python.org/dev/peps/pep-0020/)
- [Dev Cheney: Zen of Go](https://dave.cheney.net/2020/02/23/the-zen-of-go)
- [Sandi Metz](https://sandimetz.com/)
- [Kent C Dodds](https://kentcdodds.com)
- [Martin Fowler](https://martinfowler.com)
- [Dan Abramov](https://overreacted.io/)
- [Bob Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) (Not saying I agree with his political views)
- [wiki.c2.com](https://wiki.c2.com/)
- [sapegin/washingcode-book](https://github.com/sapegin/washingcode-book/)
- [trekhleb/state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode)
- [droogans/unmaintainable-code](https://github.com/Droogans/unmaintainable-code)


## 🧘 The Bare Minimum

### Recognize when the computer is smarter than you

1. Statically analyze your code with [`ESLint`](https://eslint.org/). Enable the [`rule-of-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) and `exhaustive-deps` rule to catch `React`-specific errors.
2. [`Typescript`](https://www.typescriptlang.org/) will make your life so much easier.
3. [`NextJS`](https://nextjs.org/) is an awesome framework.
4. [Be honest about your dependencies](https://overreacted.io/a-complete-guide-to-useeffect/#two-ways-to-be-honest-about-dependencies). Fix `exhaustive-deps` warnings / errors on your `useMemo`'s, `useCallback`'s and `useEffect`'s. You can try ["The latest ref pattern"](https://epicreact.dev/the-latest-ref-pattern-in-react) to keep your callbacks always up-to-date without unnecessary rerenders.
5. [Always add keys](https://epicreact.dev/why-react-needs-a-key-prop) whenever you use `map` to display components. 
6. [Only call hooks at the top level](https://reactjs.org/docs/hooks-rules.html). Don’t call Hooks inside loops, conditions, or nested functions.
7. Understand the warning "Can't perform state update on unmounted component". [See PR: facebook/react/pull/22114](https://github.com/facebook/react/pull/22114), [Reddit/u/free_username17](https://www.reddit.com/r/reactjs/comments/pvwb6m/comment/heevt8g)
8. There is a reason why errors and warnings are displayed in the console. 
9.  [Prettier](https://prettier.io/) (or an alternative) formats your code for you, giving you consistent formatting every time. You no longer need to think about it!
10. I highly recommend [Code Climate](https://codeclimate.com/quality/)  (or similar) for open-source repositories or if you can afford it. I find that automatically detecting code smells truly motivates me to reduce technical debts of the application I'm working on!
11. [`tree-shaking`](https://webpack.js.org/guides/tree-shaking/) is your friend! 
12. Prevent the ["white screen of death"](https://kentcdodds.com/blog/use-react-error-boundary-to-handle-errors-in-react) by adding several [error boundaries](https://reactjs.org/docs/error-boundaries.html) at different levels of your application. You can also use them to send alerts to an error monitoring service such as [Sentry](https://sentry.io) if you want to.
13. [`"use strict"`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode). It's 20201.

### Code is just a necessary evil

> "The best code is no code at all. Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." -  Eric S. Raymond

> "I hate code and I want as little of it as possible in our product" - Jack Diederich

> "If I had more time, I would have written a shorter letter" - Blaise Pascal, Mark Twain, among others..

See also: [Write Less Code - Richard Hariss (Svelte)](https://svelte.dev/blog/write-less-code), [Washing Code: Code is evil - Artem Sapegin](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

**TL;DR**

1. Think first before adding another dependency
2. Eliminate code with techniques not unique to `React`
3. Don't be clever. YAGNI!

#### Think first before adding another dependency

Needless to say, the more you add dependencies, the more code you ship to the browser. Ask yourself, are you actually using the features which make a particular library great? 

1. Do you really need [`Redux`](https://redux.js.org/)? It's possible. But keep in mind that React is already a [state management library](https://kentcdodds.com/blog/application-state-management-with-react). 
2. Do you really need [`Apollo client`](https://www.apollographql.com/docs/react/) ? Apollo client has many awesome features, like manual normalization. However, it will significantly increase your bundle size. If your application only makes use of features that are not unique to Apollo client , consider using a smaller library such as [`react-query`](https://react-query.tanstack.com/comparison) or [`SWR`](https://github.com/vercel/swr) (or none at all).
3. [`Axios`](https://github.com/axios/axios)? Axios is a great library with features that are not easily replicable with native `fetch`. But if the only reason for using Axios is that it has a better looking API, then consider just using a wrapper on top of fetch(such as [`redaxios`](https://github.com/developit/redaxios)). Determine whether or not your application is actually using Axios's best features.
4. [`Lodash`](https://lodash.com/)/[`underscoreJS`](https://underscorejs.org/)? [you-dont-need/You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore) 
5. [`MomentJS`](https://momentjs.com/)? [you-dont-need/You-Dont-Need-Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs)
6. You might not need `Context` for theming (`light` and `dark` mode), consider using [`css variables`](https://epicreact.dev/css-variables) instead.
7. You might not even need `Javascript`. CSS is powerful. [you-dont-need/You-Dont-Need-JavaScript](https://github.com/you-dont-need/You-Dont-Need-JavaScript)

#### Eliminate code with techniques not unique to `React`

`React` is just `Javascript` and `Javascript` is just code

1. Simplify [complex conditionals](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Avoid_conditions.md) and exit early if you can. 
2. If there is no discernable performance difference, replace traditional loops with chained higher-order functions (`map`, `filter`, `find`, `findIndex`, `some`, etc)

#### Don't be clever. YAGNI!

> "What could happen with my software in the future? Oh yeah, maybe this and that. Let’s implement all these things since we are working on this part anyway. That way it’s future-proof."

You Aren't Gonna Need It! Always implement things when you actually need them, never when you just foresee that you may need them.

See also: [Martin Fowler: YAGNI](https://martinfowler.com/bliki/Yagni.html), [C2 Wiki: You Arent Gonna Need It!](https://wiki.c2.com/?YouArentGonnaNeedIt), [C2: YAGNI original](http://c2.com/xp/YouArentGonnaNeedIt.html), [Jack Diederich: Stop Writing Classes](https://www.youtube.com/watch?v=o9pEzgHorH0)


### `React` is just `code`

Detect code smells and do something about them if you need to.

<details>
 <summary> 🙈 Examples of easy-to-catch code smells</summary>

- ❌ Methods or functions defined with a high number of arguments
- ❌ Boolean logic that may be hard to understand
- ❌ Excessive lines of code within a single file
- ❌ Duplicate code which is syntactically identical (but may be formatted differently)
- ❌ Functions or methods that may be hard to understand
- ❌ Classes defined with a high number of functions or methods
- ❌ Excessive lines of code within a single function or method
- ❌ Functions or methods with a high number of return statements
- ❌ Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)

</details>


### Just because it works, doesn't mean it is right

**TIP: Remember that you may not need to put your `state` as a dependency because you can pass a callback function instead.**
You don't need to put `setState` (from `useState`) and `dispatch` (from `useReducer`) in your dependency array for hooks like `useEffect` and `useCallback`. ESLint will NOT complain because React guarantees their stability. 

🙈 Example
 
```tsx
❌ Not-so-good
const decrement = useCallback(() => setCount(count - 1), [setCount, count]) 
const decrement = useCallback(() => setCount(count - 1), [count]) 

✅ BETTER
const decrement = useCallback(() => setCount(count => (count - 1)), [])      
```

**TIP: If your `useMemo` or `useCallback` doesn't have a dependency, you might be using it wrong.**

<details>
    <summary>🙈 Example</summary>
 
 ```tsx
 ❌ Not-so-good
const MyComponent = () => {
  const functionToCall = useCallback(x: string => `Hello ${x}! I am actually doing more than this`,[])
  const iAmAConstant = useMemo(() => { return {x: 5, y: 2} }, [])
  /* I will use functionToCall and iAmAConstant */
}
        
✅ BETTER 
const I_AM_A_CONSTANT =  { x: 5, y: 2 }
  const functionToCall = (x: string => `Hello ${x}! I am actually doing more than this`)
  const MyComponent = () => {
   /* I will use functionToCall and I_AM_A_CONSTANT */
}

 ```
</details>

## 🧘 Design for happiness

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." - Martin Fowler

> "The ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read." ― Robert C. Martin

**TL;DR**

1. 💖 Avoid state management complexity by removing redundant states 
2. 💖 Pass the banana, not the gorilla holding the banana and the entire jungle (prefer passing primitives as props)
3. 💖 Keep your components small and simple- the single responsibility principle!
4. 💖 Duplication is far cheaper than the wrong abstraction (avoid premature / inappropriate generalization)
5. Avoid prop drilling by using composition ([KCD: Prop Drilling](https://kentcdodds.com/blog/prop-drilling)). `Context` is not the solution for every state sharing problem 
6. Split giant `useEffect`s to smaller independent ones ([KCD: Myths about useEffect](https://epicreact.dev/myths-about-useeffect))
7. Extract logic to hooks and helper functions
8. To break a large component, it might be a good idea to have `logical` and `presentational` components (but not always)
9. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo`, and `useEffect`
10. Do not put too many dependencies in `useCallback`, `useMemo`, and `useEffect` 
11. For simplicity, instead of having many `useStates`, consider using `useReducer` if some values of your state rely on other values of your state and previous state

### 💖 Avoid state management complexity by removing redundant states

When you have redundant states, some states may fall out of sync; you may forget to update them given a complex sequence of interactions.
Aside from avoiding `synchronization bugs`, you'd notice that it's also easier to reason about and require less code.
See also: [KCD: Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe](https://epic-react-exercises.vercel.app/react/hooks/1)
 
##### 🙈 Example 1

You are tasked to display properties of each right triangle from a list
- the lengths of each of the three sides
-  the perimeter
-  the area

A list of two numbers `{a: number, b: number}[]` should be fetched from an API. The two numbers represent the two shorter sides of a right triangle. 

<details>
  <summary> ❌ Not-so-good Solution </summary>

```tsx    
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useTriangles<{a: number, b: number}>([])
  const [hypotenuses, setHypotenuses] = useState<number[]>([])
  const [perimeters, setPerimeters] = useState<number[]>([])
  const [areas, setAreas] = useState<number[]>([])

  useEffect(() => {
    fetchTriangles().then(r => { 
      setTriangleInfo(r)
      setHypotenuses(r.map(t => computeHypotenuse(t.a, t.b))  
      setArea(r.map(t => computeArea(t.a, t.b))  
    })
  }, [])

  useEffect(() => {
      setHypotenuses(triangleInfo.map(t => computeHypotenuse(t.a, t.b))  
      setArea(triangleInfo.map(t => computeArea(t.a, t.b))  
  }, [triangleInfo])

  useEffect(() => {
    const p = triangleInfo((t, i) => {
      return computePerimeter(t.a, t.b, hypotenuse[i])
    })
  }, [triangleInfo, hypotenuses])

  /*** show info here ****/
}
```

</details> 

<details>
  <summary> ✅ Better Solution </summary>

 ```tsx
 const TriangleInfo = () => {
   const [triangleInfo, setTriangleInfo] = useTriangles<{a: number, b: number}>([])
 
   useEffect(() => {
     fetchTriangles().then(r => setTriangleInfo(r))
   }, [])
   
   const areas = triangleInfo.map(t => computeArea(t.a, t.b))
   const hypotenuses = triangleInfo.map(t => computeHypotenuse(t.a, t.b))
   const perimeters = triangleInfo.map((t, i) => computePerimeters(t.a, t.b, hypotenuses[i]))
   
   /*** show info here ****/
 }
 ```  
</details> 
  
##### 🙈 Example 2

Suppose you are assigned to design a component which:
1. Fetches a list of unique points from an API
2. Includes a button to either sort by `x` or `y` (ascending order)
3. Includes a button to change the `maxDistance` (increase + 10)
4. Only displays the points that are NOT farther than the current `maxDistance` from the origin `(0, 0)` 
  
<details>
  <summary> ❌ Not-so-good Solution </summary>
  
```tsx
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x' 
const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [filteredPoints, setFilteredPoints] = useState<{x: number, y: number}[]>([])
  const [sortedPoints, setSortedPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(Infinity)
  const [sortBy, setSortBy] = useState<SortBy>('x')
  
  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  
  useEffect(() => {
    setSortedPoints(sortPoints(points, sortBy))
  }, [sortBy, points])

  useEffect(() => {
    setFilteredPoints(sortedPoints.filter(p => getDistance(p.x, p.y) < maxDistance))
  }, [sortedPoints, maxDistance])

  const otherSortBy = toggle(sortBy)
  
  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>Sort by: {otherSortBy}<button>
      <button onClick={() => setMaxDistance(maxDistance + 5)}>Increase max distance<button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{filteredPoints.map(p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>}
    </>

  )
}
```
</details>

<details>
  <summary> ✅ Better Solution </summary>

```tsx
  
// NOTE: You can also use useReducer instead

type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(Infinity)
  const [sortBy, setSortBy] = useState<SortBy>('x')
  
  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  
  const otherSortBy = toggle(sortBy)
  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>Sort by: {otherSortBy} <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>Increase max distance<button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{
        sortPoints(
          points.filter(p => getDistance(p.x, p.y) < maxDistance), 
          sortBy
        ).map(p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
      }
       
    </>
  )
}
```
</details>

### 💖 Pass the banana, not the gorilla holding the banana and the entire jungle

>  You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. - Joe Armstrong, creator of Erlang

To avoid falling into this trap, it's a good idea to pass mostly primitives (`boolean`, `string`, `number`, etc) types as props. (Passing primitives is also a good idea if you want to use `React.memo` for optimization)
      
> A component should just know enough to do its job and nothing more. As much as possible, components should be able to collaborate with others without knowing what they are and what they do.
          
When we do this, the components will be loosely coupled. Loose coupling means that the degree of dependency between two components is low. Loose coupling makes it easier to change, replace, or remove components without affecting other components. See also: [stackoverflow:2832017](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)

##### 🙈 Example

Create a `UserCard` component that displays two components: `Summary` and `SeeMore`. The `SeeMore` component includes presenting the `age` and `bio` of the `user`. Include a button to toggle between showing and hiding the `age` and `bio` of the `user`.

The `Summary` component displays the profile picture of the user and also his `title`, `firstName` and `lastName` (e.g. `Mr. Vincenzo Cassano`). Clicking the user's name should take you to the user's personal site. The `Summary` component may also have other functionalities. (Say for example, randomly  changing the font, size of the image, and background color whenever this component is clicked.. for brevity let's call this "the random styling feature")

The `UserCard` calls the hook `useUser` that returns an object with the type below.
        
```ts
type User = {
  firstName: string
  lastName: string
  title: string
  imgUrl: string
  webUrl: string
  age: number
  bio: string
  /****** 100 or more fields ******/
}
```
<details>
  <summary>❌ Not-so-good solution</summary>
  
```tsx

const Summary = ({ user } : { user: User }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={user.imgUrl} />
       <a href={user.webUrl}>{user.title}. {user.firstName} {user.lastName}</a>
    </>
  )
}

const SeeMore = ({ user }: { user: User }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>See more</button>
      {seeMore && <>AGE: {user.age} | BIO: {user.bio}</>}
    </>
  )
}


const UserCard = () => {
  const user = useUser()
  return <><Summary user={user} /><SeeMore user={user} /></>
}
 
```
        
</details>
        

<details>
  <summary>✅ Better solution</summary>
  
```tsx

const Summary = ({ imgUrl, webUrl, displayName }: { imgUrl: string, webUrl: string, displayName: string }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={imgUrl} />
      <a href={webUrl}>{displayName}</a>
    </>
  )
}

const SeeMore = ({ componentToShow }: {componentToShow: ReactNode }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>See more</button>
      {seeMore && <>{componentToShow}</>}
    </>
  )
}


const UserCard = () => {
  const { title, firstName, lastName, webUrl, imgUrl, age, bio } = useUser()
  return (
    <>
      <Summary displayName={`${title}. ${firstName} ${lastName}`} {...{imgUrl, webUrl}} />
      <SeeMore componentToShow={<>AGE: {age} | BIO: {bio}</>} />
    </>
  )     
}     
```
        
</details>

### 💖 Keep your components small and simple

(The paragraphs below is based on my 2015 article: [Three things I learned from Sandi Metz’s book as a non-Ruby programmer](https://medium.com/@mithi/review-sandi-metz-s-poodr-ch-1-4-wip-d4daac417665))
 
**What is the single responsibility principle?**

> A component should have one and **only one** job. It should do the smallest possible useful thing. It only has responsibilities that fulfill its purpose. 
 
A component with various responsibilities is difficult to reuse. If you want to reuse some but not all of a its behavior, it's almost always impossible to just get what you need. It is also likely to be entangled with other code. Components that do one thing which isolate that thing from the rest of your application allows change without consequence and reuse without duplication.

**How to know if your component has a single responsibility?**

> Try to describe that component in one sentence. If it is only responsible for one thing then it should be simple to describe. If it uses the word ‘and’ or ‘or’ then it is likely that your component fails this test. 
 
Inspect the component's states, the props and hooks it consumes, as well as variables and methods declared inside the component (They shouldn't be too many). Ask yourself: Do these things actually work together to fulfill the component's purpose? If some of them don't, consider moving those somewhere else or breaking down your big component to smaller ones. 

##### 🙈 Example

The requirement is to display special kinds of buttons you can click to shop for items of a specific category. For example, the user can select bags, chairs, and food.
- Each button opens a modal you can use to select and "save" items
- If the user has "saved" selected items in a specific category, that category said to be "booked"
- If it is booked, the button will have a checkmark
- You should be able to edit your booking (add or delete items) even if that category is booked
- If the user is hovering the button it should also display `WavingHand` component
- A button should also be disabled when no items for that specific category is available
- When a user hovers a disabled button, a tooltip should show "Not Available"
- If the category has no items available, the button's background should be `grey`
- If the category is booked, the button's background should be `green`
- If the category has available items and is not booked, the button's background should be `red`
- For each category, it's corresponding button has a unique label and icon
<details>
    <summary>❌ Not-so-good solution</summary>

```tsx
type ShopCategoryTileProps = {
  isBooked: boolean
  icon: ReactNode
  label: string
  componentInsideModal?: ReactNode
  items?: {name: string, quantity: number}[]
}

const ShopCategoryTile = ({
  icon,
  label,
  items
  componentInsideModal,
}: ShopCategoryTileProps ) => {
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
  const disabled = !items || items.length  === 0   
  return (
    <>
      <Tooltip title="Not Available" show={disabled}>
        <StyledButton
          className={disabled ? "grey" : isBooked ? "green" : "red" }
          disabled={disabled}
          onClick={() => disabled ? null : setOpenDialog(true) }
          onMouseEnter={() => disabled ? null : setHover(true)}
          onMouseLeave={() => disabled ? null : setHover(false)}
        >
          {icon}
          <StyledLabel>{label}<StyledLabel/>
          {!disabled && isBooked && <FaCheckCircle/>}
          {!disabled && hover && <WavingHand />}
        </StyledButton>
      </Tooltip>
      {componentInsideModal && 
        <Dialog open={openDialog} onClose={() => setOpenDialog(false)}>
          {componentInsideModal}
        </Dialog>
      }
    </>
  )
} 
```

</details>
          
<details>
    <summary>✅ Better solution</summary>

```tsx
// split into two smaller components!
const DisabledShopCategoryTile = ({ icon, label }: { icon: ReactNode, label: string }) => {
  return (
    <Tooltip title="Not available">
      <StyledButton disabled={true} className="grey"> 
          {icon} <StyledLabel>{label}<StyledLabel/>
      </Button>
    </Tooltip>
  )
}

type ShopCategoryTileProps = {
  isBooked: boolean
  icon: ReactNode
  label: string
  componentInsideModal: ReactNode
}

const ShopCategoryTile = ({
  icon,
  label,
  isBooked,
  componentInsideModal,
}: ShopCategoryTileProps ) => {
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
      
  return (
    <>
      <StyledButton
        disabled={false}
        className={isBooked ? "green" : "red"}
        onClick={() => setOpenDialog(true) }
        onMouseEnter={() => setHover(true)}
        onMouseLeave={() => setHover(false)}
      >
        {icon}
        <StyledLabel>{label}<StyledLabel/>
        {isBooked && <FaCheckCircle/>}
        {hover && <WavingHand />}
      </StyledButton>
      <Dialog open={openDialog} onClose={() => setOpenDialog(false)}>
        {componentInsideModal}
      </Dialog>
    </>
  )
}
```

</details>

Note: This is a simplified version of a component that I've actually seen in production

<details>
    <summary>❌ Not-so-good solution</summary>

```tsx
const ShopCategoryTile = ({ item, offers }: { item: ItemMap, offers?: Offer}) => {
  const dispatch = useDispatch()
  const location = useLocation()
  const history = useHistory()
  const { items } = useContext(OrderingFormContext)
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
  const isBooked =
    !item.disabled &&
    !!items?.some((a: Item) => a.itemGroup === item.group)
  const isDisabled = item.disabled || !offers
  const RenderComponent = item.component
  useEffect(() => {
    if (openDialog && !location.pathname.includes('item')) {
      setOpenDialog(false)
    }
  }, [location.pathname])
  const handleClose = useCallback(() => {
    setOpenDialog(false)
    history.goBack()
  }, [])
  return (
    <GridStyled xs={6} sm={3} md={2} item booked={isBooked} disabled={isDisabled}>
      <Tooltip
        title="Not available"
        placement="top"
        disableFocusListener={!isDisabled}
        disableHoverListener={!isDisabled}
        disableTouchListener={!isDisabled}
      >
        <PaperStyled disabled={isDisabled} elevation={isDisabled ? 0 : hover ? 6 : 2}>
          <Wrapper
            onClick={() => {
              if (isDisabled) {
                return
              }
              dispatch(push(ORDER__PATH))
              setOpenDialog(true)
            }}
            disabled={isDisabled}
            onMouseEnter={() => !isDisabled && setHover(true)}
            onMouseLeave={() => !isDisabled && setHover(false)}
          >
            {item.icon}
            <Typography variant="button">{item.label}</Typography>
            <CheckIconWrapper>{isBooked && <FaCheckCircle size="26" />}</CheckIconWrapper>
          </Wrapper>
        </PaperStyled>
      </Tooltip>
      <Dialog
        fullScreen
        open={openDialog}
        onClose={handleClose}
      >
        {RenderComponent && (
          <RenderComponent item={item} offer={offers} onClose={handleClose} />
        )}
      </Dialog>
    </GridStyled>
  )
}
```
    
</details>    

### 💖 Duplication is far cheaper than the wrong abstraction

See also: [Sandi Metz: The Wrong Abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction), [KCD: AHA Programming](https://kentcdodds.com/blog/aha-programming), [C2 Wiki: Contrived Interfaces](https://wiki.c2.com/?ContrivedInterfaces), [C2 Wiki: Expensive Setup](), [C2 Wiki: Premature Generalization](https://wiki.c2.com/?PrematureGeneralization), [Expensive Set Up Smell](https://wiki.c2.com/?ExpensiveSetUpSmell)
        
Avoid premature / inappropriate generalization. If your implementation for a simple feature requires a huge overhead, consider other options.
        
## 🧘 Performance tips
       
> Premature optimization is the root of all evil - Tony Hoare (popularized by Donald Knuth) 

**TL;DR**

1. **If you think it’s slow, prove it with a benchmark.** "In the face of ambiguity, refuse the temptation to guess."
2. Know the terms [`lazy loading`](https://nextjs.org/docs/advanced-features/dynamic-import) and [`bundle/code splitting`](https://reactjs.org/docs/code-splitting.html)
3. Use `useMemo` mostly just for expensive calculations
4. For `React.memo`, `useMemo`, `useCallback` for reducing re-renders, they shouldn't have many dependencies and the dependencies should be mostly primitive types
5. Make sure your `React.memo`, `useCallback` and `useMemo` is doing what you think it's doing (is it really preventing rerendering?)
6. Window large lists (with [tannerlinsley/react-virtual](https://github.com/tannerlinsley/react-virtual) or similar)
7. Put `Context` as low as possible in your component tree. `Context` does not have to be global to your whole app
8. `Context` should be logically separated, do not add to many values in one context provider
9. You can optimize `context` by separating the `state` and the `dispatch` function
10. Stop punching yourself everytime you blink (fix slow renders before fixing rerenders)
11. Putting your state as close as possible to where it's being used will make your app faster
12. If you're going to use a package for your forms I recommend [`react-hook-forms`](https://react-hook-form.com/). I think it is a great balance of good performance and good developer experience.

<details>
    <summary>Selected KCD articles about performance</summary>

- [KCD: State Colocation will make your React app faster](https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster)
- [KCD: When to `useMemo` and `useCallback`](https://kentcdodds.com/blog/usememo-and-usecallback)
- [KCD: Fix the slow render before you fix the re-render](https://kentcdodds.com/blog/fix-the-slow-render-before-you-fix-the-re-render)
- [KCD: Profile a React App for Performance](https://kentcdodds.com/blog/profile-a-react-app-for-performance)
- [KCD: How to optimize your context value](https://kentcdodds.com/blog/how-to-optimize-your-context-value)
- [KCD: How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
- [KCD: One React Mistake that is slowing you down](https://epicreact.dev/one-react-mistake-thats-slowing-you-down)
- [KCD: One simple trick to optimize React re-renders](https://kentcdodds.com/blog/optimize-react-re-renders)
</details>
        
## 🧘 Testing principles

>  Write tests. Not too many. Mostly integration. - Guillermo Rauch, creator of Socket.io (and other awesome things)

**TL;DR**

1. Your tests should always resemble the way your software is used
2. Stop testing implementation details
3. If your tests don't make you confident that you didn't break anything, then they didn't do their (one and only) job 
4. For the front-end, you don't need 100% code coverage, about 70% is okay
5. You should very rarely have to change tests when you refactor code
6. I like using [Jest](https://jestjs.io/), [React testing library](https://testing-library.com/docs/react-testing-library/intro/), [Cypress](https://www.cypress.io/), and [Mock service worker](https://github.com/mswjs/msw)

<details>
    <summary>Selected KCD articles about testing</summary>

- [KCD: Testing Implementation Details](https://kentcdodds.com/blog/testing-implementation-details)
- [KCD: Stop mocking fetch](https://kentcdodds.com/blog/stop-mocking-fetch)
- [KCD: Common mistakes with React Testing Library](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)
- [KCD: Making your UI tests resilient to change](https://kentcdodds.com/blog/making-your-ui-tests-resilient-to-change)
- [KCD: Write fewer, longer tests](https://kentcdodds.com/blog/write-fewer-longer-tests)
- [KCD: Write tests. Not too many. Mostly integration.](https://kentcdodds.com/blog/write-tests)
- [KCD: How to know what to test](https://kentcdodds.com/blog/how-to-know-what-to-test)
- [KCD: Common Testing Mistakes](https://kentcdodds.com/blog/common-testing-mistakes)
- [KCD: Why you've been bad about testing](https://kentcdodds.com/blog/why-youve-been-bad-about-testing)
- [KCD: Demystifying Testing](https://kentcdodds.com/blog/demystifying-testing)
- [KCD: UI Testing Myths](https://kentcdodds.com/blog/ui-testing-myths)
- [KCD: Effective Snapshot Testing](https://kentcdodds.com/blog/effective-snapshot-testing)

</details>
