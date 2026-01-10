---
created: 2023-09-29T06:26:45
aliases:
  - react hooks
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Hooks]]

[[React useEffect|useEffect]]
[[React useState|useState]]
[[React useReducer|useReducer]]
[[React useRef|useRef]]
[[React useMemo|useMemo]]
[[React useCallback|useCallback]]

## The rules of Hooks

- A Hook can only be called at the top level of a function component. So, a Hook can’t be called in a loop or in a nested function such as an event handler.
- A Hook can’t be called conditionally.
- A Hook can only be used in function components and not class components.