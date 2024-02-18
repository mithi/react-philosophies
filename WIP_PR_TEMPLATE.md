🚧 🚧 🚧 This article is a WORK IN PROGRESS (DRAFT) 🚧 🚧 🚧 

Ideally, your PR should not include too many changes. Split a huge PR to several small once so that it's easier to quickly find any  regressions might be introduced by your code.  

# Pledge of Code Quality 

- ✅ To the best of my ability, I have made sure that the code I have written is as simple and as straight forward as possible.

- ✅ I have kept the following in mind as I was writing my code
  - ✅ Single Responsibility Principle to avoid god components and methods
  - ✅ Loose Coupling, Sependency Injection, Complex logic simplification 
  - ✅ Component Composition model for crafting reusable code
  - ✅ The PR Checklist (https://gist.github.com/mithi/2ed103e3068fd7460485ecd418d78bd0)

- ✅ I have tested for cross-browser compatibility (Firefox, Safari, Chrome)

- ✅ When applicable, I have made sure to add necessary comments that explains the "why" of introduced code.

- ✅ I have taken at least 10 minutes to review the file diffs of this PR on Github and made sure the build is passing before asking someone for review. 

# `PR_TEMPLATE` based on PR type


Please ensure that you use the appropriate PR template below depending on the type of your PR.

Type: 
1. New Feature / Components
2. Bug Fix 
3. UX / Performance Enhancement
4. Refactors for Maintainability (no change in functionality)
5. Other 

## Common Sections for all PR types

Any PR type should include the following:  


1. Briefly describe the change in this PR in five bullet points or less.

2. Write down anything else the reviewer needs to know such as particular design decisions that are not that simple or straight-forward 

3. Paste the `Pledge of Code Quality` checklist below, and tick the boxes. 


## `PR_TEMPLATE` for Refactors for Maintainability

1. What techniques have you utilized in this refactor? (example: Simplifying complex logic, breaking down to smaller functions and components, extracting helper functions and common logic). Why does your refactor improve the code base? Make a case why your refactor should be merged. 

2. Write down the test cases your did make sure your refactor did not introduce any regressions. For larger refactors, write down step-by-step instructions that the reviewer can take to help increase confidence that your PR did not introduce any regressions.


## `PR_TEMPLATE` for New Feature / Components

1. Add a short screen recording showcasing the new feature. 

2. Are any existing old components are affected by this change? How? Ideally, old components should not have too many changes to avoid regressions / tight coupling and to ensure maintainability of our apps. You may be asked to put those changes in a separate PR ("Refactor for Maintainability") and merge that one before this PR can be reviewed. 

3. Add screenshots for the following states
 
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

2. Provide 2 short screen recordings (or screenshot) showcasing before and after of your change. 


## `PR_TEMPLATE` for Other

See "Common Sections for all PR types" above
