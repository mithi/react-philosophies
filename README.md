# Table of contents
0. Introduction
1. The Bare Minimum
2. Design for happiness
3. Performance tips 
4. Testing principles
5. Readings

Note: 
As I was writing this, I realized that it was actually difficult for me to separate my thoughts into the `design`, `performance`, and `testing`. I noticed that a lot of designs aimed for maintainability also makes your application faster. How cool is that?


# Introduction 
`react-philosophies` is:
- things I think about before I write my code in React.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve overtime as I my experience grows.

A lot of these things may feel like very basic and common sense but I've worked with many large complex applications that seem to... well, not care.

`react-philosophies` is inspired by various places I've stumbled upon at different points of my coding journey, 
most notably:

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

If there's something that you think should be part of my reading list, or you have great ideas that you think I should include here, don't hesitate to submit a PR or an issue; I'll check it out.


# The Bare Minimum

## This might sound crazy but a lot of times, the computer is smarter than you
1. Use ESLint including `rule-of-hooks` and `exhaustive-deps`
2. Do NOT ignore exhaustive-deps warnings for `useMemo`, `useCallback` and `useEffect`
3. Remember to add keys whenever you use `map` to display components
4. Do NOT ignore the warning "Can't perform state update on unmounted component."
5. If you see a warning or error in the console, Do not ignore it.
6. Use Prettier to automatically format your code
7. Use code climate or something similar to detect code smells

## Code is just a necessary evil

> The best code is no code at all Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." -  Eric S. Raymond

> "If I Had More Time, I Would Have Written a Shorter Letter" - Attributed to Blaise Pascal, Mark Twain, among others..

See also: 
- [Write Less Code - Richard Hariss (Svelte)](https://svelte.dev/blog/write-less-code)
- [Washing Code: Code is evil - [Artem Sapegin]](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)
- Premature Generalization
- Expensive Setup

**TLDR:**
1. Think first before adding another dependency (loadash, fetching library, redux)
2. Use `map`, `filter` if you can
3. Simplify complex conditionals

## Don't just do something, stand there
> “Any fool can write code that a computer can understand. Good programmers write code that humans can understand.” - Martin Fowler
> “Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read” ― Robert C. Martin

# Designing for happiness

**TLDR:**
1. Derive states to avoid state management complexity
2. Pass the banana, not the gorilla and the entire jungle
3. Separate concerns with the single responsibility principle
4. `logical` and `presentational` components
5. Duplication is far cheaper than the wrong abstraction
6. Avoid prop drilling by using composition
7. Prefer passing primitives as props
8. Breakdown `useEffect`s
9. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo` and `useEffect`
10. Do not put too many dependencies in `useCallback`, `useMemo` and `useEffect`
11. `Context` is not the solution for every state sharing problem

# Performance tips
> Premature optimization is the root of all evil 

**TLDR:**
1. Measure first with the React profiler
3. Splitting code to bundles
4. `useMemo` for expensive calculations
5. `React.memo` for reducing re-renders
6.  Make sure your `useCallback` and `useMemo` is doing what you think it's doing
7. Window large lists
8. `Context` does not have to be global to your whole app
9. `Context` should be logically separated
10. You can optimize `context` by separating the `state` and `dispatch` function
11. Stop punching yourself everytime you blink

# Testing principles

**TLDR:**
1. The more your tests resemble the way your software is used, the more confidence they can give you. - Kent C Dodds
2. Stop testing implementation details 
3. You don't need 100% code coverage, about 70% is okay
