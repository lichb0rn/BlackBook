---
created: 2023-09-30T07:07:47
aliases:
  - useMemo
tags:
  - type/note
topic: "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React useMemo]]

The memo Hook creates a memoized value and is beneficial for values that have computationally expensive calculations. The Hook is called `useMemo` and the syntax is as follows:
```typescript
const memoizedValue = useMemo(() => expensiveCalculation(), []);
```
A function that returns the value to memoize is passed into `useMemo` as the first argument. The function in this first argument should perform the expensive calculation. The second argument passed to `useMemo` is an array of dependencies. So, if the `expensiveCalculation` function has dependencies `a `and `b`, the call will be as follows:
```typescript
const memoizedValue = useMemo(
	() => expensiveCalculation(a, b),
	[a, b]
);
```
