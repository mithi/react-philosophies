# react-philosophies

[![Epic React Exercises](https://img.shields.io/badge/Epic%20-React%20Exercises-orange.svg?logo=react&color=0abde3)](https://github.com/mithi/epic-react-exercises) [![buy me coffee](https://img.shields.io/badge/Buy%20me%20-coffee!-orange.svg?logo=buy-me-a-coffee&color=795548)](https://ko-fi.com/minimithi) [![PRs welcome!](https://img.shields.io/badge/%20📝%20Contributions-welcome-orange.svg?style=flat)](https://github.com/mithi/react-philosophies/issues) ![Forever a work in progress!](https://img.shields.io/badge/%20🚧%20Forever%20🚧%20%20-under%20construction-yellow.svg)

If `react-philosophies` helped you in some way, consider [buying me a few cups of coffee ☕☕☕](https://ko-fi.com/minimithi). This motivates me to create more `React` "stuff"! 🙂

## Table of Contents

0. [Introduction](#-0-introduction)
1. [The Bare Minimum](#-1-the-bare-minimum)
2. [Design for happiness](#-2-design-for-happiness)
3. [Performance tips](#-3-performance-tips)
4. [Testing principles](#-4-testing-principles)
5. [Insights shared by others](#-5-insights-shared-by-others)

<details>
    <summary>The way this document is organized</summary>

<br/>
It was actually difficult for me to separate my thoughts into the `design`, `performance`, and `testing`. I noticed that lot of designs intended for maintainability also make your application faster and easier to test. Apologies if the discussion appears to be cluttered at times.
<br/>

</details>

<details>
    <summary><strong>Thanks for all the PRs 🚜, coffee ☕, recommended readings 📚, and sharing of ideas 💡 (View contributors)</strong></summary>

---
    
**💡 Comments, suggestions, violent reactions? I'd love to hear them!**

If there's something that you think should be part of my reading list or/and if you have great ideas that you think I should include here, don't hesitate to submit a PR or an issue. Particularly, I've included the section [`Insights shared by others`](#-5-insights-shared-by-others), should you wish to add your own ideas 🙂. Broken links, grammar, formatting, and typographical error corrections are also welcome. Any contributions to improve `react-philosophies` whether big or small are always appreciated.

---
    

**💡 Special thanks to those who took the time to share their thoughts!**
- The [`r/reactjs`](https://www.reddit.com/r/reactjs/comments/pvwb6m/what_i_think_about_when_i_write_code_in_react) community
- [Josh W Comeau](https://www.joshwcomeau.com/) (Check out his amazing course on [CSS](https://css-for-js.dev/))
- [@unpunnyfuns](https://github.com/unpunnyfuns)
- [@cassidoo](https://github.com/cassidoo)

**☕ Coffee!**

- [Myles](https://Ko-fi.com/home/coffeeshop?txid=0fac8f5b-994e-4208-b767-7872a9e2519e&mode=public&img=ogsomeoneboughtme)
- [Daniel](https://Ko-fi.com/home/coffeeshop?txid=7d71404a-fa0c-419d-9808-46ea520c913f&mode=public&img=ogsomeoneboughtme)
- [Ankit](https://Ko-fi.com/home/coffeeshop?txid=8c1254ef-0e5a-43a0-8475-e3567e2c8dab&mode=public&img=ogbuymeacoffee)

**🚜 Pull Requests**

- [@fengzilong](https://github.com/fengzilong)
- [@ankitwww](https://github.com/ankitwww)
- [@dzakki](https://github.com/dzakki)
- [@metonym](https://github.com/metonym)
- [@sapegin](https://github.com/sapegin)

**📚 Readings recommended to me**

- [ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript), [3rs-of-software-architecture](https://github.com/ryanmcdermott/3rs-of-software-architecture), [ryanmcdermott/code-review-tips](https://github.com/ryanmcdermott/code-review-tips)
- [Ben Moseley and Peter Marks: Out of the Tar Pit (2006)](http://curtclifton.net/papers/MoseleyMarks06a.pdf), recommended by [@icyjoseph](https://github.com/icyjoseph)
- [`goldbergyoni/nodebestpractices`](https://github.com/goldbergyoni/nodebestpractices), recommended by [@rstacruz](https://github.com/rstacruz)
- [Dan Abramov: Writing Resilient Components](https://overreacted.io/writing-resilient-components/), recommended by [Mon Quindoza](https://ph.linkedin.com/in/monquindoza)
- [Matthieu Kern: Stop checking if your component is mounted](https://medium.com/doctolib/react-stop-checking-if-your-component-is-mounted-3bb2568a4934), recommended by [@Pierre-CLIND](https://github.com/Pierre-CLIND)
    
</details>

## 🧘 0. Introduction

`react-philosophies` is:

- things I think about when I write `React` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve over time as my experience grows
- mostly techniques which are variations of basic [refactoring](https://en.wikipedia.org/wiki/Code_refactoring) methods, [SOLID](https://en.wikipedia.org/wiki/SOLID) principles, and [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming) ideas... just applied to `React` specifically 🙂

A lot of these things may feel like very basic and common-sense. But surprisingly, I've worked with large complex applications where these things are not taken into consideration. The examples I present here are based on code I have actually seen in production.

`react-philosophies` is inspired by various places I've stumbled upon at different points of my coding journey.

Here are a few of them:

- [Tim Peters: Zen of Python (Pep 20)](https://www.python.org/dev/peps/pep-0020/)
- [Dev Cheney: Zen of Go](https://dave.cheney.net/2020/02/23/the-zen-of-go)
- [Sandi Metz](https://sandimetz.com/)
- [Kent C Dodds](https://kentcdodds.com)
- [trekhleb/state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode), [droogans/unmaintainable-code](https://github.com/Droogans/unmaintainable-code), [sapegin/washingcode-book](https://github.com/sapegin/washingcode-book/), [wiki.c2.com](https://wiki.c2.com/)

> As a seasoned developer I have certain quirks, opinions, and common patterns that I fall back on. Having to explain to another person why I am approaching a problem in a particular way is really good for helping me break bad habits and challenge my assumptions, or for providing validation for good problem solving skills. - [Coraline Ada Ehmke](https://where.coraline.codes)

## 🧘 1. The Bare Minimum

### 1.1 Recognize when the computer is smarter than you

1. Statically analyze your code with [`ESLint`](https://eslint.org/). Enable the [`rule-of-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) and `exhaustive-deps` rule to catch `React`-specific errors.
2. Enable ["strict"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) mode. It's 2021. 
3. [Be honest about your dependencies](https://overreacted.io/a-complete-guide-to-useeffect/#two-ways-to-be-honest-about-dependencies). Fix `exhaustive-deps` warnings / errors on your `useMemo`'s, `useCallback`'s and `useEffect`'s. You can try ["The latest ref pattern"](https://epicreact.dev/the-latest-ref-pattern-in-react) to keep your callbacks always up-to-date without unnecessary rerenders.
4. [Always add keys](https://epicreact.dev/why-react-needs-a-key-prop) whenever you use `map` to display components.
5. [Only call hooks at the top level](https://reactjs.org/docs/hooks-rules.html). Don’t call Hooks inside loops, conditions, or nested functions.
6. Understand the warning "Can't perform state update on unmounted component". [See PR: facebook/react/pull/22114](https://github.com/facebook/react/pull/22114), [Reddit/u/free_username17](https://www.reddit.com/r/reactjs/comments/pvwb6m/comment/heevt8g)
7. Prevent the ["white screen of death"](https://kentcdodds.com/blog/use-react-error-boundary-to-handle-errors-in-react) by adding several [error boundaries](https://reactjs.org/docs/error-boundaries.html) at different levels of your application. You can also use them to send alerts to an error monitoring service such as [Sentry](https://sentry.io) if you want to. ([Accounting for Failures In React](https://brandondail.com/posts/fault-tolerance-react))
8. There is a reason why errors and warnings are displayed in the console.
9. Remember [`tree-shaking`](https://webpack.js.org/guides/tree-shaking/)!
10. [Prettier](https://prettier.io/) (or an alternative) formats your code for you, giving you consistent formatting every time. You no longer need to think about it!
11. [`Typescript`](https://www.typescriptlang.org/) will make your life so much easier.
12. I highly recommend [Code Climate](https://codeclimate.com/quality/) (or similar) for open-source repositories or if you can afford it. I find that automatically-detected code smells truly motivates me to reduce the technical debts of the application I'm working on!
13. [`NextJS`](https://nextjs.org/) is an awesome framework.

### 1.2 Code is just a necessary evil

> "The best code is no code at all. Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." - Eric S. Raymond

> "I hate code and I want as little of it as possible in our product" - Jack Diederich

> "If I had more time, I would have written a shorter letter" - Blaise Pascal, Mark Twain, among others..

See also: [Write Less Code - Richard Harris (Svelte)](https://svelte.dev/blog/write-less-code), [Washing Code: Code is evil - Artem Sapegin](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

**TL;DR**

1. Think first before adding another dependency
2. Eliminate code with techniques not unique to `React`
3. Don't be clever. YAGNI!

#### 1.2.1 Think first before adding another dependency

Needless to say, the more you add dependencies, the more code you ship to the browser. Ask yourself, are you actually using the features which make a particular library great?

<details>
    <summary><strong><em>🙈  Do you really need it?</strong> View examples of dependencies / code you might not need</em></summary>

<br/>

1. Do you really need [`Redux`](https://redux.js.org/)? It's possible. But keep in mind that React is already a [state management library](https://kentcdodds.com/blog/application-state-management-with-react).

2. Do you really need [`Apollo client`](https://www.apollographql.com/docs/react/) ? Apollo client has many awesome features, like manual normalization. However, it will significantly increase your bundle size. If your application only makes use of features that are not unique to Apollo client , consider using a smaller library such as [`react-query`](https://react-query.tanstack.com/comparison) or [`SWR`](https://github.com/vercel/swr) (or none at all).

3. [`Axios`](https://github.com/axios/axios)? Axios is a great library with features that are not easily replicable with native `fetch`. But if the only reason for using Axios is that it has a better looking API, then consider just using a wrapper on top of fetch (such as [`redaxios`](https://github.com/developit/redaxios) or your own). Determine whether or not your application is actually using Axios's best features.

4. [`Lodash`](https://lodash.com/)/[`underscoreJS`](https://underscorejs.org/)? [you-dont-need/You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore)

5. [`MomentJS`](https://momentjs.com/)? [you-dont-need/You-Dont-Need-Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs)

6. You might not need `Context` for theming (`light`/`dark` mode), consider using [`css variables`](https://epicreact.dev/css-variables) instead.

7. You might not even need `Javascript`. CSS is powerful. [you-dont-need/You-Dont-Need-JavaScript](https://github.com/you-dont-need/You-Dont-Need-JavaScript)
<br/>

</details>

#### 1.2.2 Eliminate code with techniques not unique to `React`

`React` is just `Javascript` and `Javascript` is just code

1. Simplify [complex conditionals](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Avoid_conditions.md) and exit early if you can.
2. If there is no discernable performance difference, replace traditional loops with chained higher-order functions (`map`, `filter`, `find`, `findIndex`, `some`, etc)

#### 1.2.3 Don't be clever. YAGNI!

> "What could happen with my software in the future? Oh yeah, maybe this and that. Let’s implement all these things since we are working on this part anyway. That way it’s future-proof."

**Y**ou **A**ren't **G**onna **N**eed **I**t! Always implement things when you actually need them, never when you just foresee that you may need them.

See also: [Martin Fowler: YAGNI](https://martinfowler.com/bliki/Yagni.html), [C2 Wiki: You Arent Gonna Need It!](https://wiki.c2.com/?YouArentGonnaNeedIt), [C2: YAGNI (original)](http://c2.com/xp/YouArentGonnaNeedIt.html), [Jack Diederich: Stop Writing Classes](https://www.youtube.com/watch?v=o9pEzgHorH0)

### 1.3 Leave it better than you found it

**Detect code smells and do something about them if you need to**. 

If you recognize that something is wrong, fix it right then and there. But if it's not that easy to fix or you don't have time to fix it at that moment, at least add a comment (`FIXME` or `TODO`) with a concise explanation of the identified problem. Make sure everybody knows it is broken. It shows others that you care and that they should also do the same when they encounter those kinds of things.

<details>
    <summary><strong>🙈 View examples of easy-to-catch code smells</strong></summary>

- ❌ Methods or functions defined with a large number of arguments
- ❌ Boolean logic that may be hard to understand
- ❌ Excessive lines of code within a single file
- ❌ Duplicate code which is syntactically identical (but may be formatted differently)
- ❌ Functions or methods that may be hard to understand
- ❌ Classes / Components defined with a large number of functions or methods
- ❌ Excessive lines of code within a single function or method
- ❌ Functions or methods with a large number of return statements
- ❌ Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)

</details>

Keep in mind that code smells don't necessarily mean that code should be changed. A code smell just informs you that you might be able to think of a better way to implement the same functionality.

### 1.4 You can do better

**💁‍♀️ TIP: Remember that you may not need to put your `state` as a dependency because you can pass a callback function instead.**

You don't need to put `setState` (from `useState`) and `dispatch` (from `useReducer`) in your dependency array for hooks like `useEffect` and `useCallback`. ESLint will NOT complain because React guarantees their stability.

🙈 Example

```tsx
❌ Not-so-good
const decrement = useCallback(() => setCount(count - 1), [setCount, count])
const decrement = useCallback(() => setCount(count - 1), [count])

✅ BETTER
const decrement = useCallback(() => setCount(count => (count - 1)), [])
```

**💁‍♀️ TIP: If your `useMemo` or `useCallback` doesn't have a dependency, you might be using it wrong.**

<details>
    <summary>🙈 View example</summary>
 
 <br />
 
 ```tsx
 ❌ Not-so-good
const MyComponent = () => {
    const functionToCall = useCallback(x: string => `Hello ${x}!`,[])
    const iAmAConstant = useMemo(() => { return {x: 5, y: 2} }, [])
    /* I will use functionToCall and iAmAConstant */
}
        
✅ BETTER 
const I_AM_A_CONSTANT =  { x: 5, y: 2 }
const functionToCall = (x: string => `Hello ${x}!`)
const MyComponent = () => {
    /* I will use functionToCall and I_AM_A_CONSTANT */
}

````
</details>

**💁‍♀️ TIP: Wrapping your custom context with a hook creates a better-looking API**

Not only does it look better, but you also only have to import one thing instead of two.

<details>
    <summary>🙈 View example</summary>

 <br />

❌ Not-so-good
```tsx
// you need to import two things every time 
import { useContext } from "react"
import { SomethingContext } from "some-context-package"

function App() {
  const something = useContext(SomethingContext) // looks okay, but could look better
  // blah
}
```

✅  Better
```tsx
  
// on one file you declare this hook
function useSomething() {
  const context = useContext(SomethingContext)
  if (context === undefined) {
    throw new Error('useSomething must be used within a SomethingProvider')
  }
  return context
}
  
// you only need to import one thing each time
import { useSomething } from "some-context-package"

function App() {
  const something = useSomething() // looks better
  // blah
}  
```

</details>

**💁‍♀️ TIP: [`README Driven Development`](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) is a [cool concept](https://rathes.me/blog/en/readme-driven-development/)!**

You don't have to follow RDD religiously, but the idea behind it is great. I find that when I first write the API (how the component will be used) before implementing it, this usually creates a better designed component than when I don't.

> If your software solves the wrong problem or nobody can figure out how to use it, there’s something very bad going on. Until you’ve written about your software, you have no idea what you’ll be coding. -Tom Preston-Werner

## 🧘 2. Design for happiness

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." - Martin Fowler

> "The ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read." ― Robert C. Martin [(Not saying I agree with his political views)](https://techexplained.substack.com/p/tech-bullshit-explained-uncle-bob)

**TL;DR**

1. 💖 Avoid state management complexity by removing redundant states
2. 💖 Pass the banana, not the gorilla holding the banana and the entire jungle (prefer passing primitives as props)
3. 💖 Keep your components small and simple - the single responsibility principle!
4. 💖 Duplication is far cheaper than the wrong abstraction (avoid premature / inappropriate generalization)
5. Avoid prop drilling by using composition ([Michael Jackson](https://www.youtube.com/watch?v=3XaXKiXtNjw)). `Context` is not the solution for every state sharing problem
6. Split giant `useEffect`s to smaller independent ones ([KCD: Myths about useEffect](https://epicreact.dev/myths-about-useeffect))
7. Extract logic to hooks and helper functions
8. To break a large component, it might be a good idea to have `logical` and `presentational` components (but not necessarily, use your best judgement)
9. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo`, and `useEffect`
10. Do not put too many dependencies in `useCallback`, `useMemo`, and `useEffect`
11. For simplicity, instead of having many `useState`s, consider using `useReducer` if some values of your state rely on other values of your state and previous state
12. `Context` does not have to be global to your whole app. Put `Context` as low as possible in your component tree. Do this the same way you put variables, comments, states (and code in general) as close as possible to where they're relevant / being used.

### 💖 2.1 Avoid state management complexity by removing redundant states

When you have redundant states, some states may fall out of sync; you may forget to update them given a complex sequence of interactions.
Aside from avoiding synchronization bugs, you'd notice that it's also easier to reason about and require less code.
See also: [KCD: Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe](https://epic-react-exercises.vercel.app/react/hooks/1)

##### 🙈 Example 1

You are tasked to display properties of a right triangle
- the lengths of each of the three sides
- the perimeter
- the area

The triangle is an object with two numbers `{a: number, b: number}` that should be fetched from an API. 
The two numbers represent the two shorter sides of a right triangle.

<details>
 <summary> ❌ View not-so-good Solution </summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = use<{a: number, b: number} | null>(null)
  const [hypotenuse, setHypotenuse] = useState<number | null>(null)
  const [perimeter, setPerimeter] = useState<number | null>(null)
  const [areas, setArea] = useState<number | null>(null)

  useEffect(() => {
    fetchTriangle().then(t => setTriangleInfo(t))
  }, [])

  useEffect(() => {
    if(!triangleInfo) {
      return
    }
    
    const { a, b } = triangleInfo
    const h = computeHypotenuse(a, b)
    setHypotenuse(h)
    const newArea = computeArea(a, b)
    setArea(newArea)
    const p = computePerimeter(a, b, h)
    setPerimeter(p)

  }, [triangleInfo])

  if (!triangleInfo) {
    return null
  }

  /*** show info here ****/
}
````

</details>

<details>
  <summary> ✅ View "better" solution </summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useState<{
    a: number;
    b: number;
  } | null>(null)

  useEffect(() => {
    fetchTriangle().then((r) => setTriangleInfo(r))
  }, []);

  if (!triangleInfo) {
    return
  }

  const { a, b } = triangeInfo
  const area = computeArea(a, b)
  const hypotenuse = computeHypotenuse(a, b))
  const perimeter = computePerimeter(a, b, hypotenuse)
 
  /*** show info here ****/
};
```

</details> 
  
##### 🙈 Example 2

Suppose you are assigned to design a component which:

1. Fetches a list of unique points from an API
2. Includes a button to either sort by `x` or `y` (ascending order)
3. Includes a button to change the `maxDistance` (increase by `10` each time, initial value should be `100`)
4. Only displays the points that are NOT farther than the current `maxDistance` from the origin `(0, 0)`
5. Assume that the list only has 100 items (meaning you don't need to worry about optimization). If you're working with really large numbers of items, you can memoize some computations with `useMemo`.

<details>
  <summary> ❌ View a not-so-good Solution </summary>
  
```tsx
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [filteredPoints, setFilteredPoints] = useState<{x: number, y: number}[]>([])
  const [sortedPoints, setSortedPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')
  
  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  
  useEffect(() => {
    const sorted = sortPoints(points, sortBy)
    setSortedPoints(sorted)
  }, [sortBy, points])

  useEffect(() => {
    const filtered = sortedPoints.filter(p => getDistance(p.x, p.y) < maxDistance)
    setFilteredPoints(filtered)
  }, [sortedPoints, maxDistance])

  const otherSortBy = toggle(sortBy)
  const pointToDisplay = filteredPoints.map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy}
      <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}

````
</details>

<details>
  <summary> ✅ View a "better" Solution </summary>

```tsx

// NOTE: You can also use useReducer instead
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')

  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  

  const otherSortBy = toggle(sortBy)
  const filtedPoints = points.filter(p => getDistance(p.x, p.y) < maxDistance)
  const pointToDisplay = sortPoints(filteredPoints, sortBy).map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy} <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}
````

</details>

### 💖 2.2 Pass the banana, not the gorilla holding the banana and the entire jungle

> You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. - Joe Armstrong, creator of Erlang

To avoid falling into this trap, it's a good idea to pass mostly primitives (`boolean`, `string`, `number`, etc) types as props. (Passing primitives is also a good idea if you want to use `React.memo` for optimization)

> A component should just know enough to do its job and nothing more. As much as possible, components should be able to collaborate with others without knowing what they are and what they do.

When we do this, the components will be loosely coupled. Loose coupling means that the degree of dependency between two components is low. Loose coupling makes it easier to change, replace, or remove components without affecting other components. See also: [stackoverflow:2832017](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)

##### 🙈 Example

Create a `MemberCard` component that displays two components: `Summary` and `SeeMore`.
The `MemberCard` takes in the prop `id` . The `MemberCard` consumes the hook `useMember` which takes in an `id` and returns the corresponding `Member` information.

```ts
type Member = {
  id: string
  firstName: string
  lastName: string
  title: string
  imgUrl: string
  webUrl: string
  age: number
  bio: string
  /****** 100 more fields ******/
}
```

The `SeeMore` component should display the `age` and `bio` of the `member`.
Include a button to toggle between showing and hiding the `age` and `bio` of the `member`.

The `Summary` component displays the picture of the `member`. 
It also displays his `title`, `firstName` and `lastName` (e.g. `Mr. Vincenzo Cassano`). 
Clicking the `member`'s name should take you to the `member`'s personal site.
The `Summary` component may also have other functionalities. 
(Example, whenever this component is clicked...
the font, size of the image, and background color are randomly changed...
for brevity let's call this "the random styling feature")

<details>
  <summary>❌ View a not-so-good solution</summary>
  
```tsx

const Summary = ({ member } : { member: Member }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={member.imgUrl} />
      <a href={member.webUrl} >
        {member.title}. {member.firstName} {member.lastName}
      </a>
    </>
  )
}

const SeeMore = ({ member }: { member: Member }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>
        See {seeMore ? "less" : "more"}
      </button>
      {seeMore && <>AGE: {member.age} | BIO: {member.bio}</>}
    </>
  )
}

const MemberCard = ({ id }: { id: string })) => {
  const member = useMember(id)
  return <><Summary member={member} /><SeeMore member={member} /></>
}

````

</details>


<details>
  <summary>✅ View a "better" solution</summary>

```tsx

const Summary = ({ imgUrl, webUrl, header }: { imgUrl: string, webUrl: string, header: string }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={imgUrl} />
      <a href={webUrl}>{header}</a>
    </>
  )
}

const SeeMore = ({ componentToShow }: { componentToShow: ReactNode }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>
        See {seeMore ? "less" : "more"}
      </button>
      {seeMore && <>{componentToShow}</>}
    </>
  )
}


const MemberCard = ({ id }: { id: string }) => {
  const { title, firstName, lastName, webUrl, imgUrl, age, bio } = useMember(id)
  const header = `${title}. ${firstName} ${lastName}`
  return (
    <>
      <Summary {...{ imgUrl, webUrl, header }} />
      <SeeMore componentToShow={<>AGE: {age} | BIO: {bio}</>} />
    </>
  )
}
````

</details>
    
Notice that in the `✅  "better" solution"`, `SeeMore` and `Summary` are components that can be used not just by `Member`. It can be used perhaps by other objects such as `CurrentUser`, `Pet`, `Post`... anything that needs those specific functionality.

### 💖 2.3 Keep your components small and simple

**What is the single responsibility principle?**

> A component should have one and **only one** job. It should do the smallest possible useful thing. It only has responsibilities that fulfill its purpose.

A component with various responsibilities is difficult to reuse. If you want to reuse some but not all of its behavior, it's almost always impossible to just get what you need. It is also likely to be entangled with other code. Components that do one thing which isolate that thing from the rest of your application allows change without consequence and reuse without duplication.

**How to know if your component has a single responsibility?**

> Try to describe that component in one sentence. If it is only responsible for one thing then it should be simple to describe. If it uses the word ‘and’ or ‘or’ then it is likely that your component fails this test.

Inspect the component's state, the props and hooks it consumes, as well as variables and methods declared inside the component (there shouldn't be too many). Ask yourself: Do these things actually work together to fulfill the component's purpose? If some of them don't, consider moving those somewhere else or breaking down your big component into smaller ones.

(The paragraphs above are based on my 2015 article: [Three things I learned from Sandi Metz’s book as a non-Ruby programmer](https://medium.com/@mithi/review-sandi-metz-s-poodr-ch-1-4-wip-d4daac417665))

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
    <summary>❌ View a not-so-good solution</summary>

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
    <summary>✅ View a "better" solution</summary>

```tsx
// split into two smaller components!

const DisabledShopCategoryTile = ({ icon, label }: { icon: ReactNode, label: string }) => {
  return (
    <Tooltip title="Not available">
      <StyledButton disabled={true} className="grey">
        {icon}
        <StyledLabel>{label}<StyledLabel/>
      </Button>
    </Tooltip>
  )
}

type ShopCategoryTileProps = {
  icon: ReactNode
  label: string
  isBooked: boolean
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
      {openDialog &&
        <Dialog onClose={() => setOpenDialog(false)}>
          {componentInsideModal}
        </Dialog>
      }}
    </>
  )
}
```

</details>

Note: The example above is a simplified version of a component that I've actually seen in production

<details>
    <summary>❌ View a not-so-good solution</summary>

```tsx
const ShopCategoryTile = ({
  item,
  offers,
}: {
  item: ItemMap;
  offers?: Offer;
}) => {
  const dispatch = useDispatch();
  const location = useLocation();
  const history = useHistory();
  const { items } = useContext(OrderingFormContext)
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
  const isBooked =
    !item.disabled && !!items?.some((a: Item) => a.itemGroup === item.group)
  const isDisabled = item.disabled || !offers
  const RenderComponent = item.component

  useEffect(() => {
    if (openDialog && !location.pathname.includes("item")) {
      setOpenDialog(false)
    }
  }, [location.pathname]);
  const handleClose = useCallback(() => {
    setOpenDialog(false)
    history.goBack()
  }, [])

  return (
    <GridStyled
      xs={6}
      sm={3}
      md={2}
      item
      booked={isBooked}
      disabled={isDisabled}
    >
      <Tooltip
        title="Not available"
        placement="top"
        disableFocusListener={!isDisabled}
        disableHoverListener={!isDisabled}
        disableTouchListener={!isDisabled}
      >
        <PaperStyled
          disabled={isDisabled}
          elevation={isDisabled ? 0 : hover ? 6 : 2}
        >
          <Wrapper
            onClick={() => {
              if (isDisabled) {
                return;
              }
              dispatch(push(ORDER__PATH));
              setOpenDialog(true);
            }}
            disabled={isDisabled}
            onMouseEnter={() => !isDisabled && setHover(true)}
            onMouseLeave={() => !isDisabled && setHover(false)}
          >
            {item.icon}
            <Typography variant="button">{item.label}</Typography>
            <CheckIconWrapper>
              {isBooked && <FaCheckCircle size="26" />}
            </CheckIconWrapper>
          </Wrapper>
        </PaperStyled>
      </Tooltip>
      <Dialog fullScreen open={openDialog} onClose={handleClose}>
        {RenderComponent && (
          <RenderComponent item={item} offer={offers} onClose={handleClose} />
        )}
      </Dialog>
    </GridStyled>
  )
}
```

</details>

### 💖 2.4 Duplication is far cheaper than the wrong abstraction

Avoid premature / inappropriate generalization. If your implementation for a simple feature requires a huge overhead, consider other options.
I highly recommend reading [Sandi Metz: The Wrong Abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction).

See also: [KCD: AHA Programming](https://kentcdodds.com/blog/aha-programming), [C2 Wiki: Contrived Interfaces](https://wiki.c2.com/?ContrivedInterfaces), [C2 Wiki: The Expensive Setup Smell](https://wiki.c2.com/?ExpensiveSetUpSmell), [C2 Wiki: Premature Generalization](https://wiki.c2.com/?PrematureGeneralization)

        
## 🧘 3. Performance tips

> Premature optimization is the root of all evil - Tony Hoare (popularized by Donald Knuth)

**TL;DR**

1. **If you think it’s slow, prove it with a benchmark.** _"In the face of ambiguity, refuse the temptation to guess."_ The profiler of [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) (Chrome extension) is your friend!
2. Use `useMemo` mostly just for expensive calculations
3. Use `React.memo`, `useMemo`, and `useCallback` for reducing re-renders, they shouldn't have many dependencies and the dependencies should be mostly primitive types
4. Make sure your `React.memo`, `useCallback` or `useMemo` is doing what you think it's doing (is it really preventing rerendering?)
5. Stop punching yourself every time you blink (fix slow renders before fixing rerenders)
6. Putting your state as close as possible to where it's being used will not only make your code so much easier to read but It would also make your app faster (state colocation)
7. `Context` should be logically separated, do not add to many values in one context provider. If any of the values of your context changes, all components consuming that context also rerenders even if those components don't use the specific value that was actually changed.
8. You can optimize `context` by separating the `state` and the `dispatch` function
9. Know the terms [`lazy loading`](https://nextjs.org/docs/advanced-features/dynamic-import) and [`bundle/code splitting`](https://reactjs.org/docs/code-splitting.html)
10. Window large lists (with [`tannerlinsley/react-virtual`](https://github.com/tannerlinsley/react-virtual) or similar)
11. A smaller bundle size usually also means a faster app. You can visualize the code bundles you've generated with tools such as [`source-map-explorer`](https://create-react-app.dev/docs/analyzing-the-bundle-size/) or [`@next/bundle-analyzer`](https://www.npmjs.com/package/@next/bundle-analyzer) (for NextJS).
12. If you're going to use a package for your forms, I recommend [`react-hook-forms`](https://react-hook-form.com/). I think it is a great balance of good performance and good developer experience.

<details>
    <summary><strong>View selected KCD articles about performance</strong></summary>


- [KCD: State Colocation will make your React app faster](https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster)
- [KCD: When to `useMemo` and `useCallback`](https://kentcdodds.com/blog/usememo-and-usecallback)
- [KCD: Fix the slow render before you fix the re-render](https://kentcdodds.com/blog/fix-the-slow-render-before-you-fix-the-re-render)
- [KCD: Profile a React App for Performance](https://kentcdodds.com/blog/profile-a-react-app-for-performance)
- [KCD: How to optimize your context value](https://kentcdodds.com/blog/how-to-optimize-your-context-value)
- [KCD: How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
- [KCD: One React Mistake that is slowing you down](https://epicreact.dev/one-react-mistake-thats-slowing-you-down)
- [KCD: One simple trick to optimize React re-renders](https://kentcdodds.com/blog/optimize-react-re-renders)

</details>

## 🧘 4. Testing principles

> Write tests. Not too many. Mostly integration. - Guillermo Rauch, creator of Socket.io (and other awesome things)

**TL;DR**

1. Your tests should always resemble the way your software is used
2. Make sure that you're not testing implementation details - things which users do not use, see, or even know about
3. If your tests don't make you confident that you didn't break anything, then they didn't do their (one and only) job
5. You'll know you implemented correct tests when you rarely have to change tests when you refactor code given the same user behavior
5. For the front-end, you don't need 100% code coverage, about 70% is probably good enough. Tests should make you more productive not slow you down. Maintaining tests can slow you down. You get dimishing returns on adding more tests after a certain point
6. I like using [Jest](https://jestjs.io/), [React testing library](https://testing-library.com/docs/react-testing-library/intro/), [Cypress](https://www.cypress.io/), and [Mock service worker](https://github.com/mswjs/msw)
        
<details>
    <summary><strong>View selected KCD articles about testing</strong></summary>

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

## 🧘 5. Insights shared by others

If you'd like to share some of the things you think about when you write React code that I didn't touch upon, you can submit a PR and add them to this section. 
Thanks for taking the time to share your ideas! 
        
### [Josh W Comeau](https://www.joshwcomeau.com/) 

> A similar principle I feel much more strongly about is not to pass _setters_ that have too much power. For example, I might pass an `updateEmail` function instead of a `setUser` function. I don't want random components to be able to _change_ things they don't have any business changing.

> Not only should a component have a single responsibility, it should also have a clear spot on the spectrum of abstraction. On one end, we have generic building blocks like `<Button>`, `<Heading>`, `<Modal>`. On the other end, we have one-off templates like `<Homepage>` and `<ContactForm>`. Every component should have a clear spot on this spectrum. A `<Button>` component shoudn't have a _user_ prop, since users are a higher-abstract concept and `Button` is a low-abstract component.

(Note, the above is taken from his response to my email... I really appreciate that he took the time to share his ideas 🙂)
