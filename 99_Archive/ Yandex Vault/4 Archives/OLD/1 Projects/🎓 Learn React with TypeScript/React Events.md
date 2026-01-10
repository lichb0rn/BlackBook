---
created: 2023-09-27T11:22:17
aliases:
  - react events
  - react custom event
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Events]]

Events in [[React]] events are very similar to browser native events. In fact, React events are a wrapper on top of the browser’s native events.

Event handlers in React are generally registered to an element in [[JSX]] using an attribute. The following code snippet registers a `click` event handler called `handleClick` on a button element:
```jsx
<button onClick={handleClick}>...</button>
```
## Example
```javascript
// Alert.js
import { useState } from "react";

export function Alert({
	type = "information",
	heading,
	children,
	closable,
	onClose
}) {
	const [visible, setVisible] = useState(true);
	if (!visible) return null;
	const handleCloseClick = () => {
		setVisible(false);
		if (onClose) onClose();
	};
	return (
	<div>
		<div>
			<span
				role="img"
				aria-label={type === "warning" ? "Warning" : "Information">							
			{type === "warning" ? "⚠️" : "ℹ️"}
			</span>
			<span>{heading}</span>
		</div>
		{closable && (
			<button aria-label="Close" onClick={handleCloseClick}>
				<span role="img" aria-label="Close">
					❌
				</span>
			</button>
		)}
		<div>{children}</div>
	</div>
	);
}

// App.js
import { Alert } from "./Alert";
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <Alert
        type="information"
        heading="Success"
        closable
        onClose={() => console.log("closed")}
      >
        All is fine!
      </Alert>
    </div>
  );
}
```
В данном примере `onClose` - custom react event.