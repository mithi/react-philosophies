🚧 🚧 🚧 This document is a work in progress  🚧 🚧 🚧

# 🧘 Table of contents
0. [Introduction](#-0-introduction)
1. [The Bare Minimum](#-1-the-bare-minimum)
2. [Design for happiness](#-2-design-for-happiness)
3. [Performance tips](#-3-performance-tips)
4. [Testing principles](#-4-testing-principles)

Note: 
As I was writing this, I realized that it was actually difficult for me to separate my thoughts into the `design`, `performance`, and `testing`. I noticed that a lot of designs aimed for maintainability also makes your application faster. How cool is that?

# 🧘 0. Introduction 
`react-philosophies` is:
- things I think about before I write `React` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve overtime as my experience grows
- mostly techniques which are variations of basic refactoring methods, SOLID principles, and extreme programming ideas just applied to React specifically.

A lot of these things may feel like very basic and common-sense. However, I've worked with many large complex applications written by people who seem to... well... not care. The examples I've presented here are based on code I have actually seen in production. 

`react-philosophies` is inspired by various places I've stumbled upon at different points of my coding journey.

Most notably:

- [Tim Peters: Zen of Python (Pep 20)](https://www.python.org/dev/peps/pep-0020/)
- [Dev Cheney: Zen of Go](https://dave.cheney.net/2020/02/23/the-zen-of-go)
- [Sandi Metz](https://sandimetz.com/)
- [Kent C Dodds](kentcdodds.com)
- [Martin Fowler](https://martinfowler.com)
- [Dan Abramov](https://overreacted.io/)
- [Bob Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) (Not saying I agree with his political views)
- [wiki.c2.com](https://wiki.c2.com/)
- [sapegin/washingcode-book](https://github.com/sapegin/washingcode-book/)
- [trekhleb/state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode)
- [droogans/unmaintainable-code](https://github.com/Droogans/unmaintainable-code)

If there's something that you think should be part of my reading list, or if you have great ideas that you think I should include here, don't hesitate to submit a PR or an issue; I'll check it out. Any contributions to improve this document where big or small is always welcome and appreciated.

# 🧘 1. The Bare Minimum

## 1.1 Recognize when the computer is smarter than you
1. Use ESLint including `rule-of-hooks` and `exhaustive-deps`
2. Typescript and NextJS will make your life SO MUCH EASIER
3. Do NOT ignore exhaustive-deps warnings / errors for `useMemo`, `useCallback` and `useEffect`
4. Remember to add keys whenever you use `map` to display components
5. Remember to NOT use hooks inside conditionals, always put them at the top
6. Do NOT ignore the warning ["Can't perform state update on unmounted component."](https://stackoverflow.com/questions/56442582/react-hooks-cant-perform-a-react-state-update-on-an-unmounted-component)
7. If you see a warning or error in the console, do not ignore it.
8. Use [Prettier](https://prettier.io/) to automatically format your code
9. Use [Code Climate](https://codeclimate.com/quality/) (or similar) to detect code smells
10. Make sure you're tree-shaking to eliminate dead code
11. Add several [error boundaries](https://reactjs.org/docs/error-boundaries.html)

## 1.2 Code is just a necessary evil

> "The best code is no code at all Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." -  Eric S. Raymond

> "If I had more time, I would have written a shorter letter" - Blaise Pascal, Mark Twain, among others..

See also: [Write Less Code - Richard Hariss (Svelte)](https://svelte.dev/blog/write-less-code), [Washing Code: Code is evil - [Artem Sapegin]](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

### TLDR
1. Think first before adding another dependency
2. Eliminate code with techniques not unique to `React`
3. You aren't gonna need it (probably)

### 1.1.1 Think first before adding another dependency

Needless to say, the more you add dependencies the more code you ship to the browser, this makes your app slow. Ask yourself, 
are you actually using the features that makes a particular library great? 

1. Do you need `Redux`? React is already a [state management library](https://kentcdodds.com/blog/application-state-management-with-react). 

2. Do you really need `Apollo client`? Apollo client has many features, especially when it comes to micromanaging and doing manual normalization. However, it significantly increases your bundle size as well. Consider using [react-query](https://react-query.tanstack.com/comparison) or [SWR](https://github.com/vercel/swr)

3. Do you need fetching libraries like `Axios`? Axios is a great library because of to keep your code clean. It also has some features that are not easily replicable with the native fetch api. But if your application is not making use of most of Axios best features and only using a handful of functions, then consider just making a wrapper on top of fetch. Especially, if the only reason is that it has a better looking API.

4. Lodash/underscore? [you-dont-need/You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore) 
5. MomentJS? [you-dont-need/You-Dont-Need-Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs)

6. You might not even need `Javascript`. CSS is powerful. [you-dont-need/You-Dont-Need-JavaScript](https://github.com/you-dont-need/You-Dont-Need-JavaScript)

### 1.1.2 Eliminate code with techniques not unique to `React`.

Always remember, `React` is just `Javascript` and `Javascript` is just code

1. Simplify [complex conditionals](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Avoid_conditions.md) and exiting early if you can. 
2. Replace most traditional loops with higher order functions (ie `reduce`, `map`, `filter`), among other techniques. See also: [you-dont-need/You-Dont-Need-Loops](https://github.com/you-dont-need/You-Dont-Need-Loops)

### 1.1.3 You aren't gonna need it (probably)

See also: [Martin Fowler: YAGNI](https://martinfowler.com/bliki/Yagni.html), [C2 Wiki: You Arent Gonna Need It!](https://wiki.c2.com/?YouArentGonnaNeedIt)

## 1.3 `React` is just `code`

Fix code smells. Most of them can be checked easily by [Code Climate](https://codeclimate.com/quality/)

<details>
 <summary> 🙈 Examples of code smells </summary>

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


## 1.4 Just because it works, doesn't mean it is right

If you have `useCallback` that depends on `setState` and `state`, it might not actually have dependencies

<details>
    <summary>🙈 Example</summary>
 
```tsx
❌ BAD
const decrement = useCallback(() => setCount(count - 1), [count]) 

✅ BETTER
const decrement = useCallback(() => setCount(count => count - 1), [])      
```

</details>


If your `useMemo` and `useCallback` doesn't have a dependency, you might be doing it wrong. 

<details>
    <summary>🙈 Example</summary>
 
 ```tsx
 ❌ BAD
const MyComponent = () => {
  const componentNeedsToCallThisFunction = useCallback(x: string => `Hello ${x}! I am actually doing more than this`,[])
  const iAmAConstant = useMemo(() => { return {x: 5, y: 2} }, [])
  /* I will use componentNeedsToCallThisFunction and iAmAConstant here */
}
        
✅ BETTER 
 const I_AM_A_CONSTANT =  { x: 5, y: 2 }
 const componentNeedsToCallThisFunction = (x: string => `Hello ${x}! I am actually doing more than this`)
 const MyComponent = () => {
      /* I will use componentNeedsToCallThisFunctions and I_AM_A_CONSTANT */
  }

 ```
</details>

# 🧘 2. Design for happiness
> “Any fool can write code that a computer can understand. Good programmers write code that humans can understand.” - Martin Fowler

> “Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read” ― Robert C. Martin

### TLDR
1. 💖 Derive states to avoid state management complexity 
2. 💖 Pass the banana, not the gorilla and the entire jungle, (prefer passing primitives as props)
3. 💖 Keep things small and simple. Separate concerns with the single responsibility principle
4. Duplication is far cheaper than the wrong abstraction (avoid premature generalization)
5. Avoid prop drilling by using composition
6. Breakdown large `useEffect`s to smaller ones
7. Extract logic to hooks and helper functions
8. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo` and `useEffect`
9. Consider using `useReducer`, when values of your state relies on other values of your state
10. Do not put too many dependencies in `useCallback`, `useMemo` and `useEffect`
11. `Context` is not the solution for every state sharing problem
12. It maybe an good idea to have `logical` and `presentational` components, if your component gets too large
13. Put your state as close as possible to where it's being used (Colocating state)
14. Use `css variables` for theming (`light` and `dark` mode) instead of `context`

## 2.1 Derive states to avoid state management complexity
When you have redundant states, some states may fall out of sync if we forget to update it given a complex sequence of interactions.
Aside from avoiding `synchronization bugs`, you'd notice that it's also easier to reason about and require less code. (Remember: Code is Evil!)
See also: [Kent C Dodd's Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe Exercises and Solution](https://epic-react-exercises.vercel.app/react/hooks/1)
 
### 🙈 Example 1
Suppose you fetch a list of two numbers `{a: number, b: number}[]`. The two numbers represent the two shorter sides 
of a right triangle. The length of the three sides, the perimeter, and the area of each triangle should be displayed

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

  /*** show here info here ****/
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
   
   /*** show here info here ****/
 }
 ```  
</details> 
  
### 🙈 Example 2
Suppose you are assigned to make a component which fetches a list of unique points
There is a button to either sort by x or y and a button to change the max distance (increase + 10)
. We filter points that farther than a specific distance from the origin `(0, 0)` 
  
<details>
  <summary> ❌ Not-so-good Solution  </summary>
  
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
      Showing only points that are less than {maxDistance} units away from origin `(0, 0)`
      Currently sorted by: {sortBy} in increasing order
      <ol>{filteredPoints.map(p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>}
    </>

  )
}
```
</details>

<details>
  <summary> ✅ Better Solution </summary>

```tsx
  
# NOTE: You might also want to consider using useReducer here

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
      Showing only points that are less than {maxDistance} units away from origin `(0, 0)`
      Currently sorted by: {sortBy} in increasing order
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

## 2.2 If you need a banana, pass the banana, not the gorilla and the entire jungle 
>  You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. - Joe Armstrong, creator of Erlang, on software reusability.

One thing that can help you with this is to pass primitives (`boolean`, `string`, `number` etc), instead of passing objects. Also, passing primitives is also a good idea because you may want to use `React.memo` in the future if you need to for optimization.

A component should just know enough to do its job and NOTHING MORE. As much as possible, components should be able to collaborate with others without knowing what they are and what they do.

### 🙈 Example
A `UserCard` component that displays a `Summary`, and `SeeMore` components. Add a button to toggle between showing and hiding the age and bio on of the user.

The `Summary` component that displays the display name (e.g. `Mr Vincenzo Cassano`) and a picture. Clicking the name display takes you to the user's personal site.
(The `Summary` component may have other functionalities like changing the font, size of the image, and background color randomly upon clicking)

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
  /****** 20 or more fields containing more information about the user ******/
}
```
<details>
  <summary>❌ Not-so-good solution</summary>
  
```tsx

const Summary = ({ user } : {user: User}) => {
  /*** include  functionality for switching image size, font, and background color randomly  upon clicking ***/
  return (
    <>
      <img src={user.imgUrl} />
       <a href={user.webUrl}>{user.title}. {user.firstName} {user.lastName}</a>
    </>
  )
}

const SeeMore = ({ user }: {user: User}) => {
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

const Summary = ({ imgUrl, webUrl, displayName }: {imgUrl: string, webUrl: string, displayName: string}) => {
   /*** include functionality for switching image size, font, and background color randomly upon clicking ***/
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
      {seeMore && <>{componentToShow }</>}
    </>
  )
}


const UserCard = () => {
  const { title, firstName, lastName, webUrl, imgUrl, age, bio} = useUser()
  return (
    <>
      <Summary displayName={`${title}. ${firstName} ${lastName}`} {...{imgUrl, webUrl}} />
      <SeeMore componentToShow={<>AGE: {age} | BIO: {ubio}</>} />
    </>
  )     
}     
```
        
</details>

## 2.3 Separate concerns with the single responsibility principle

The following is based on my old article [Three things I learned from Sandi Metz’s book as a non-Ruby programmer](https://medium.com/@mithi/review-sandi-metz-s-poodr-ch-1-4-wip-d4daac417665), but applied to React components. 
 
**What is the single responsibility principle?**
A component should have one and only one job. It should do the smallest possible useful thing. It only has responsibilities that fulfil its purpose. This matters because react applications that are easy to change consist of components that are easy to reuse. A component with various responsibilities are difficult to reuse. If you want to reuse some but not all of its behavior. It's almost always impossible to just get what you need. It is also likely to be entangled with other code. Components that do one thing which isolate that thing from the rest of your application allows change without consequence and reuse without duplication.

**How to know if your component has a single responsibility?**
> Try to describe that component in one sentence. If it is only responsible for one thing then it should be simple to describe. If it uses the word ‘and’ or ‘or’ then it is likely that your component failed this test. 

### 🙈 Example
The requirement is to have special kinds of buttons you can click to shop for items of a specific category. For example, I can select bags, chairs, and food. Each button opens a modal you can use to select items. If the user selected items of a specific category then that category is booked. If it is booked, there will the button will be green with a checkmark, else it would be red. You can still add or delete items even if that category is booked. If the user is hovering the button it should also display `WavingHand` component. The buttons can also be disabled when those items are not available. If hovered, a tooltip shows "not available". Each button has a label and an icon.

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
      <Tooltip title="Not available" show={disabled }>
        <StyledButton
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
        <Dialog open={openDialog} onClick={() => setOpenDialog(false)}>
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
// separate to two components DisabledShopCategoryTile and ShopCategoryTile
const DisabledShopCategoryTile = ({ icon, label }: { icon: ReactNode, label: string }) => {
  return (
    <Tooltip title="Not available">
      <StyledButton disabled={true} > 
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
        onClick={() => setOpenDialog(true) }
        onMouseEnter={() => setHover(true)}
        onMouseLeave={() => setHover(false)}
      >
        {icon}
        <StyledLabel>{label}<StyledLabel/>
        {isBooked && <FaCheckCircle/>}
        {hover && <WavingHand />}
      </StyledButton>
      <Dialog open={openDialog} onClick={() => setOpenDialog(false)}>
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

## 2.4 Duplication is far cheaper than the wrong abstraction

See also: [Sandi Metz: The Wrong Abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction), [Kent C Dodds: AHA Programming](https://kentcdodds.com/blog/aha-programming), [C2 Wiki: Contrived Interfaces](https://wiki.c2.com/?ContrivedInterfaces), [C2 Wiki: Expensive Setup](), [C2 Wiki: Premature Generalization](https://wiki.c2.com/?PrematureGeneralization), [Expensive Set Up Smell](https://wiki.c2.com/?ExpensiveSetUpSmell)
        
Avoid premature generalization. If your implementation for a simple feature requires a huge overhead, consider other options.
        
# 🧘 3. Performance tips
       
> Premature optimization is the root of all evil - Tony Hoare (popularized by Donald Knuth) 

### TLDR
1. If you think it’s slow, prove it with a benchmark. “In the face of ambiguity, refuse the temptation to guess.”
3. Use lazy loading
4. Use `useMemo` mostly just for expensive calculations
5. When using `React.memo` for reducing re-renders, it's better to pass only primitive props
6.  Make sure your `React.memo`, `useCallback` and `useMemo` is doing what you think it's doing (preventing rerendering)
7. Window large lists (with React virtual or similar)
8. Put `Context` as low as possible in your component tree. `Context` does not have to be global to your whole app.
9. `Context` should be logically separated, do not add to many values in one context provider
10. You can optimize `context` by separating the `state` and the `dispatch` function
11. Stop punching yourself everytime you blink (fixing slow rerenders before fixing rerenders)
       
# 🧘 4. Testing principles

### TLDR
>  Write tests. Not too many. Mostly integration. - Guillermo Rauch (creator of Socket.io)

1. Your tests should always resemble the way your software is used
2. Stop testing implementation details
3. If your tests don't make you confident that you didn't break anything, then they didn't do their (one and only) job 
4. For the front-end, you don't need 100% code coverage, about 70% is okay
5. You should very rarely have to change tests when you refactor code.
