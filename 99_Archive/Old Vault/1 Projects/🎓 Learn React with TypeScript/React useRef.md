---
created: 2023-09-30T06:53:45
aliases:
  - useRef
tags:
  - type/note
topic: "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React useRef]]

ref Hook is called `useRef` and it returns a variable whose **value is persisted for the lifetime of a component**. This means that the variable doesn’t lose its value when a component re-renders.
The value returned from the ref Hook is often referred to as a `ref`. The ref can be changed **without causing a re-render.**
```javascript
const ref = useRef(initialValue);
```
```typescript
const ref = useRef<Ref>(initialValue);
```

The value of the `ref` is accessed via its `current` property:
```javascript
console.log("Current ref value ", ref.current);
```
The value of the `ref` can be updated via its `current` property as well:
```javascript
ref.current = newValue;
```
A common use of the `useRef` Hook is to access [[064 HTML and CSS|HTML]] elements imperatively. HTML elements have a `ref` attribute in [[JSX]] that can be assigned to a `ref`. The following is an example of this:
```typescript
function MyComponent() {
	const inputRef = useRef<HTMLInputElement>(null);
	
	function doSomething() {
		console.log("All the properties and methods of the input",
		 inputRef.current);
	}
	return <input ref={inputRef} type="text" />''
}
```