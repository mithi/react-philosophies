🚧 🚧 🚧 This document is a work in progress  🚧 🚧 🚧

# 💪 Table of contents
0. Introduction
1. The Bare Minimum
2. Design for happiness
3. Performance tips 
4. Testing principles
5. Spotting a low-hanging fruit

Note: 
As I was writing this, I realized that it was actually difficult for me to separate my thoughts into the `design`, `performance`, and `testing`. I noticed that a lot of designs aimed for maintainability also makes your application faster. How cool is that?

# 💪 0. Introduction 
`react-philosophies` is:
- things I think about before I write `React` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve overtime as I my experience grows
- mostly techniques are seems like variations of basic refactoring methods, SOLID principles, and extreme programming ideas, just applied to React specifically.

A lot of these things may feel like very basic and common sense but I've worked with many large complex applications that seem to... well... not care.

`react-philosophies` is inspired by various places I've stumbled upon at different points of my coding journey.

Most notably:

- [Tim Peters: Zen of Python (Pep 20)](https://www.python.org/dev/peps/pep-0020/)
- [Dev Cheney: Zen of Go](https://dave.cheney.net/2020/02/23/the-zen-of-go)
- [Sandi Metz](https://sandimetz.com/)
- [Martin Fowler](https://martinfowler.com)
- [Kent C Dodds](kentcdodds.com)
- [Dan Abramov](https://overreacted.io/)
- [Bob Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) (Not saying I agree with his political views)
- [wiki.c2.com](https://wiki.c2.com/)
- [sapegin/washingcode-book](https://github.com/sapegin/washingcode-book/)
- [trekhleb/state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode)
- [droogans/unmaintainable-code](https://github.com/Droogans/unmaintainable-code)

If there's something that you think should be part of my reading list, or if you have great ideas that you think I should include here, don't hesitate to submit a PR or an issue; I'll check it out.

# 💪 1. The Bare Minimum

## This might sound crazy but a lot of times, the computer is smarter than you
1. Use ESLint including `rule-of-hooks` and `exhaustive-deps`
2. Do NOT ignore exhaustive-deps warnings / errors for `useMemo`, `useCallback` and `useEffect`
3. Remember to add keys whenever you use `map` to display components
4. Remember to NOT use hooks inside conditionals, always put them at the top
5. Do NOT ignore the warning ["Can't perform state update on unmounted component."](https://stackoverflow.com/questions/56442582/react-hooks-cant-perform-a-react-state-update-on-an-unmounted-component)
6. If you see a warning or error in the console, Do not ignore it.
7. Use [Prettier](https://prettier.io/) to automatically format your code
8. Use [Code Climate](https://codeclimate.com/quality/) (or similar) to detect code smells

## Code is just a necessary evil

> "The best code is no code at all Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." -  Eric S. Raymond

> "If I had more time, I would have written a shorter letter" - Attributed to Blaise Pascal, Mark Twain, among others..

See also: [Write Less Code - Richard Hariss (Svelte)](https://svelte.dev/blog/write-less-code), [Washing Code: Code is evil - [Artem Sapegin]](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

### TLDR
1. Think first before adding another dependency (loadash, fetching libraries, redux)
2. Use `map`, `filter` if you can, avoid traditional loops if you can
3. 💖 Simplify complex conditionals, and exit early if you can
5. You're probably NOT gonna need it. 
6. Avoid premature generalization
7. If your solution of an simple feature requires an expensive setup, consider other options

# 💪 2. Design for happiness
> “Any fool can write code that a computer can understand. Good programmers write code that humans can understand.” - Martin Fowler
> “Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read” ― Robert C. Martin

### TLDR
1. 💖 Derive states to avoid state management complexity 
2. 💖 Pass the banana, not the gorilla and the entire jungle, (prefer passing primitives as props)
3. 💖 Separate concerns with the single responsibility principle
4. 💖 Duplication is far cheaper than the wrong abstraction
5. Avoid prop drilling by using composition
6. Breakdown large `useEffect`s to smaller ones
7. Extract logic to hooks and helper functions
8. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo` and `useEffect`
9. Consider using `useReducer`, when some elements of your state relies on other values of your state
10. Do not put too many dependencies in `useCallback`, `useMemo` and `useEffect`
11. `Context` is not the solution for every state sharing problem
12. It maybe an good idea to have `logical` and `presentational` components, if your component gets too large
13. Practice state colocation

## 2.1 Derive states to avoid state management complexity
When you have redundant states, some states may fall out of sync if we forget to update it given a complex sequence of interactions.
Aside from avoiding `synchronization bugs`, you'd notice that it's also easier to reason about and require less code. (Remember: Code is Evil!)
See also: [Kent C Dodd's Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it).
 
### Example 1
Suppose you fetch a list of two numbers `{a: number, b: number}[]`. The two numbers represent the two shorter sides 
of a right triangle. The length of the three sides, the perimeter, and the area of each triangle should be displayed

<details>
  <summary> ❌ Bad Solution </summary>

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
  
### Example 2
Suppose you are assigned to make a component which fetches a list of unique points
There is a button to either sort by x or y and a button
to filter points that farther than a specific distance from the origin `(0, 0)` 
  
<details>
  <summary> ❌ Bad Solution  </summary>
  
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
      <button onClick={() => { setSortBy(otherSortBy)}}>Sort by: {otherSortBy} <button>
      <button onClick={() => { setMaxDistance(maxDistance + 5)}}>Increase max distance<button>
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

const pointsInfoReducer = (state: )
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
      <button onClick={() => { setSortBy(otherSortBy)}}>Sort by: {otherSortBy} <button>
      <button onClick={() => { setMaxDistance(maxDistance + 10)}}>Increase max distance<button>
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

One thing that can help you with this is to pass primitives (`boolean`, `string`, `number` etc), instead of passing objects.
Also, passing primitives is also a good idea because you may want to use `React.memo` in the future if you need to for optimization.

### Example
A `UserCard` component that displays a `Summary`, and `SeeMore` components. Add a button to toggle between showing and hiding the age and bio on of the user.

The `Summary` component that displays the display name (e.g. `Mr Vincenzo Cassano`) and a picture. Clicking the name display takes you to the user's personal site.
(The `Summary` component may have other functionalities like changing the font, size of the image, and background color randomly upon clicking)

The `UserCard` calls the hook `useUser` that return's an object with the type below.
        
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
  <summary>❌ Bad solution</summary>
  
```tsx

const Summary = ({user}: {user: User}) => {
  /*** includes functionality for switching image size, font, and background color randomly  upon clicking ***/
  return (
    <>
      <img src={user.imgUrl} />
       <a href={user.webUrl}>{user.title}. {user.firstName} {user.lastName}</a>
    </>
  )
}

const SeeMore = ({user}: {user: User}) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => { setSeeMore(!seeMore)} }>See more</button>
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

const Summary = ({ imgUrl, webUrl, displayName } : {imgUrl: string, webUrl: string, displayName: string}) => {
   /*** includes functionality for switching image size, font, and background color randomly  upon clicking ***/
  return (
    <>
      <img src={imgUrl} />
       <a href={webUrl}>{displayName}</a>
    </>
  )
}

const SeeMore = ({ age, bio } : {age: number, bio: string}) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => { setSeeMore(!seeMore)} }>See more</button>
      {seeMore && <>AGE: {age} | BIO: {bio}</>}
    </>
  )
}


const UserCard = () => {
  const { title, firstName, lastName, webUrl, imgUrl, age, bio} = useUser()
  return (
    <>
      <Summary displayName={`${title}. ${firstName} ${lastName}`} {...{imgUrl, webUrl}}/>
      <SeeMore {...{age, bio}} />
    </>
  )     
}
        
```
        
</details>

# 💪 3. Performance tips
       
> Premature optimization is the root of all evil

### TLDR
1. If you think it’s slow, prove it with a benchmark.  “In the face of ambiguity, refuse the temptation to guess.”
3. Split code to bundles
4. `useMemo` mostly just for expensive calculations
5. `React.memo` for reducing re-renders
6.  Make sure your `React.memo`, `useCallback` and `useMemo` is doing what you think it's doing (preventing rerendering)
7. Window large lists (with React virtual or similar)
8. Put `Context` as low as possible in your component tree. `Context` does not have to be global to your whole app.
9. `Context` should be logically separated
10. You can optimize `context` by separating the `state` and the `dispatch` function
11. Stop punching yourself everytime you blink (fixing slow rerenders before fixing rerenders)
       
# 4. Testing principles

### TLDR
>  Write tests. Not too many. Mostly integration. - Guillermo Rauch‏ (creator of Socket.io)

1. Your tests should always resemble the way your software is used
2. Stop testing implementation details
3. If your tests don't make you confident that you didn't break anything, then they didn't do their (one and only) job 
4. For the front-end, You don't need 100% code coverage, about 70% is okay
5. You should very rarely have to change tests when you refactor code.
       
# 💪 5. Spotting a low-hanging Fruit
Ask yourself do you really need it as a dependency?
```tsx
❌ BAD
const decrement = useCallback(() => setCount(count - 1), [count]) 

✅ BETTER
const decrement = useCallback(() => setCount(count => count - 1), [])
        
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
        
        

  
