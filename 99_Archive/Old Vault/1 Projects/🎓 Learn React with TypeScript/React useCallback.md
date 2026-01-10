---
created: 2023-09-30T07:16:07
aliases:
  - useCallback
tags:
  - type/note
topic: "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React useCallback]]

The callback Hook memoizes a function so that it isn’t recreated on each render. The Hook is called `useCallback` and the syntax is as follows:
```typescript
const memoizedCallback = useCallback(() => someFunction(), []);
```
A function that executes the function to memoize is passed into `useCallback` as the first argument. The second argument passed to `useCallback` is an array of dependencies.
When any dependencies change, the function in the first argument is executed again to return a new function to memoize.

A common use case for `useCallback` is to **prevent unnecessary re-renders of child components**.