🚧 🚧 🚧 Important: This article is a WORK IN PROGRESS (DRAFT) 🚧 🚧 🚧 

---

# Pledge of Code Quality 

- [ ] To the best of my ability, I have made sure that the code I have written is as simple and as straightforward as possible.

- [ ] I have kept the following in mind as I was writing my code:
  - [ ] The [single responsibility principle](https://github.com/mithi/react-philosophies/tree/main?tab=readme-ov-file#-23-keep-your-components-small-and-simple) to avoid god components and methods
  - [ ] Dependency Injection techniques like [render props](https://legacy.reactjs.org/docs/render-props.html) for loose coupling
  - [ ] [Component composition](https://legacy.reactjs.org/docs/composition-vs-inheritance.html) for crafting reusable code
  - [ ] [Simplifying complex logic and conditionals](https://refactoring.guru/replace-nested-conditional-with-guard-clauses) so that my code is easy to read and understand
  - [ ] Common [concrete examples of code smells](https://github.com/mithi/react-philosophies/blob/main/WIP_CODE_QUALITY_CHECKLIST.md#concrete-examples) to be wary of

- [ ] I have tested for cross-browser compatibility (Firefox, Safari, Chrome)

- [ ] When applicable, I have made sure to add necessary comments that explains the "why" of introduced code.

- [ ] I have taken at least 10 minutes to review the file diffs of this PR on Github's UI and made sure the build is passing before asking someone for review. 

# `PR_TEMPLATE` based on PR type

Please ensure that you use the appropriate PR template below depending on the type of your PR.

Type: 
1. New Feature or Components
2. Bug Fixes
3. UX or Performance Enhancement
4. Refactors for Maintainability (no change in functionality)
5. Other 

## Common Sections for all PR types

Ideally, your PR should not include too many changes. Split a huge PR to several independent loosely-coupled ones so that it's easier to quickly find any regressions that might have been introduced by your code.  

Any PR type should include the following in the description:  

1. Briefly describe the change in this PR in five sentences or less.

2. Write down anything else the reviewer needs to know such as particular design decisions that are not that simple or straightforward 

3. Paste the `Pledge of Code Quality` checklist below, and tick the boxes. 


## `PR_TEMPLATE` for Refactors for Maintainability

1. What techniques have you utilized in this refactor? (example: simplifying complex logic, breaking down to smaller functions and components, extracting helper functions and common logic). Why does your refactor improve the code base? Make a case why your refactor should be merged. 

2. Write down the test cases you tested for to make sure your refactor did not introduce any regressions. For larger refactors, write down step-by-step instructions that the reviewer can take to help increase confidence that your PR did not introduce any regressions.


## `PR_TEMPLATE` for New Features / Components

1. If applicable, add a short screen recording showcasing the new feature. 

2. Are any existing components affected by this change? How? Ideally, old components should not have too many changes to avoid regressions and tight coupling that might make it painful to modify in the future. You may be asked to put those changes in a separate PR ("Refactor for Maintainability") and merge that one before this PR can be reviewed. 

3. If applicable, add screenshots for the following states
 
| - | Mobile Screen | Laptop Screen | Wide Monitor Screen |
|--------|--------|--------|--------|
| Loading State | - | - | - |
| Usual successful completed state | - | -| -|
| Empty State (no items) | - | - | - |
| Overflow state (several items) | - | -  | - |
| Backend Errors (fetching or posting) | - | - | - | 
| Error Boundary state (unexpected / uncaught frontend error) | - | - | - | 
| backend returns or user inputs no data (e.g empty strings) | - | - | - | 
| backend returns or user inputs large data (say 100000 character strings) | - | - | - | 


## `PR_TEMPLATE` for Bug Fixes and UX / Performance Enhancement

1. Add detailed step-by-step-instructions to help the PR reviewer replicate the issue you've solved

2. Provide 2 short screen recordings (or screenshot) showcasing before and after of your change


## `PR_TEMPLATE` for Other

See "Common Sections for all PR types" above
