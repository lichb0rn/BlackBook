---
created: 2023-09-30T06:18:41
aliases:
  - useReducer
tags:
  - type/note
topic: "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React useReducer]]

`useReducer` is an alternative method of managing state. It uses a reducer function for state changes, which takes in the current state value and returns the new state value.
```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

The `dispatch` function takes in an argument that describes the change. This object is called an `action`. 
```javascript
dispatch({ type: 'add', amount: 2 })
```
Here’s an example code snippet of a reducer:
```typescript
function reducer(state: State, action: Action): State {
	switch(action.type) {
		case 'add':
			return { ...state, total: state.total + action.amount };
		case ...
			...
		default:
			return state;
	}
}
```
The `reducer` function usually contains a `switch` statement based on the `action` `type`. Each `switch` branch makes the required changes to the state and returns the updated state. A new state object is created during the state change – **the current state is never mutated.** A **mutating state would result in the component not re-rendering**.

The [[Система типов TypeScript|types]] for `useReducer` can be explicitly defined in its [[TypeScript Generics|generic]] parameter as follows:
```typescript
const [state, dispatch] = useReducer<Reducer<State, Action>>(
	reducer,
	initialState
);
```
`Reducer` is a standard [[React]] type that has generic parameters for the type of state and the type of action.

`useReducer` is more complex than [[React useState|useState]] because state changes go through a `reducer` function that we must implement. This **benefits complex state objects with related properties or when a state change depends on the previous state value**.

The [[React useState|useState]] Hook is **more appropriate when the state is based on primitive values independent of any other state**.