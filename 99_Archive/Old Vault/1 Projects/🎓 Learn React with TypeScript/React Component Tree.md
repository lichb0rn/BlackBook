---
created: 2023-09-27T10:02:59
aliases:
  - react component tree
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Component Tree]]

A React app is structured in a tree of components and DOM elements. The root component is the component at the top of the tree.

[[React components]] can be nested inside another React component. The `App` component is nested inside the `StrictMode` component in the sample project.

React components can reference one or more other components, and even [[DOM]] elements, in their [[JSX]]:
```javascript
export default function App() {
	return (
		<div className="App">
			<h1>Hello CodeSandbox</h1>
			<h2>Start editing to see some magic happen!</h2>
		</div>
	);
}
```
The component tree in the project is constructed as follows:
```
StrictMode
└── App
    └── div
         └── h1
           └── h2
```
