---
created: 2023-09-27T09:49:19
aliases:
  - react entrypoint
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Entry Point]]
```javascript
// index.js
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

const rootElement = document.getElementById("root");
const root = createRoot(rootElement);
root.render(
	<StrictMode>
		<App />
	</StrictMode>
);
```
- The first statement imports a `StrictMode` component from [[React]]. This means that the [[React strict mode|StrictMode]] component from the react library will be used later in the code in this file. We will cover import statements in detail in the next section.
- The second statement imports a `createRoot` function from [[React]].
- The third import statement imports an `App` component from the `App.js` file in our project.
- A `rootElement` variable is then assigned to a [[DOM]] element with an id of "`root`".
- React’s `createRoot` function takes in a [[DOM]] element and returns a variable that can be used to display a [[React Component Tree]]. The `rootElement` variable is then passed into `createRoot`, and the result is assigned to a `root` variable.
- The `render` function is called on the `root` variable, passing in [[JSX]] containing the `StrictMode` component with the `App` component nested inside. The `render` function displays the [[React]] components on the page. This process is often referred to as **rendering**.

>[!note]
>The [[React strict mode|StrictMode]] component will check the content inside it for potential problems and report them in the browser’s console. This is often referred to as [[React]]’s strict mode. The strict mode in React is different from the strict mode in [[JavaScript]], but their purpose of eliminating bad code is the same.

