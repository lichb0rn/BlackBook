---
created: 2023-09-27T09:12:24
aliases:
  - virtual DOM
tags:
  - type/note
topic: "[[React]]"
source: "[[Learn React with TypeScript]]"
---
[[React Components|React components]] are displayed performantly using a virtual DOM ([[DOM|Document Object Model]]). However, changes to the real DOM can be costly, leading to performance problems in an interactive app. [[React]] solves this performance problem by **using an in-memory representation of the real DOM called a virtual DOM**. Before React changes the real DOM, **it produces a new virtual DOM and compares it against the current virtual DOM to calculate the minimum amount of changes required to the real DOM**. The real DOM is then updated with those minimum changes.

