---
created: 2023-10-04T08:49:04
aliases:
  - react context
tags:
  - type/note
topic: "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React Context]]

React context is an object that can be accessed by components. This object can contain state values, so it provides a mechanism for sharing state across components.

A context is created using a `createContext` function as follows:
```ts
const SomeContext = createContext<ContextType>(defaultValue);
```
The context also contains a `Provider` component that needs to be placed above components requiring access to the context object in the [[React Component Tree|component tree]]. A provider wrapper component can be created that stores the shared state and passes it to the context `Provider` component as follows:
```jsx
export function SomeProvider({ children }: Props) {
	const [someState, setSomeState] = useState(initialState);
	return (
		<SomeContext.Provider value={{ someState }}>
			{children}
		</SomeContext.Provider>
	)
}
```
The provider wrapper component can then be placed appropriately in the component tree, above components requiring the shared state:
```jsx
function App() {
	return (
		<SomeProvider>
			<Header />
			<Main />
		</SomeProvider>
	)
}
```

React also contains a `useContext` [[React Hooks|hook]] that can be used so that the context values can be consumed as a hook, as follows:
```ts
const { someState } = useContext(SomeContext);
```