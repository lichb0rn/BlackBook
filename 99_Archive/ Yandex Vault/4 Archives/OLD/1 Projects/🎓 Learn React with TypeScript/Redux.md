---
created: 2023-10-04T09:17:25
aliases:
  - redux
tags:
  - type/note
topic: "[[State Management]]"
source:
---
# [[Redux]]

In Redux, the state lives in a centralized immutable object referred to as a `store`. There is only a single store for the whole app. Like [[React useReducer|useReducer]], the state in a store is updated by dispatching an action, which is an object containing the type of change and any data required to make the change. An action is handled by a reducer function, which creates a new version of the state.

## Installing Redux
```sh
npm i @reduxjs/toolkit react-redux
```

## Creating a store

A Redux store can be created using the Redux Toolkit’s `configureStore` function as follows:
```ts
export const store = configureStore({
	reducer: {
		someFeature: someFeatureReducer,
		anotherFeature: anotherFeatureReducer
	},
});
```
Each feature in the app can have its own area of state and reducer to change the state. The different areas of state are often referred to as **slices**. In the preceding example, there are two slices called `someFeature` and `anotherFeature`.

The Redux Toolkit has a function to create slices, called `createSlice`:
```ts
export const someSlice = createSlice({
	name: "someFeature",
	initialState,
	reducers: {
		someAction: (state) => { state.someValue = "something"; },
		anotherAction: (state) => { state.someOtherValue = "smthing else"; },
	},
});
```
The slice created from `createSlice` contains a reducer function that wraps the action handlers. This reducer function can be referenced in the reducer property of `configureStore` when the store is created:
```ts
export const store = configureStore({
  reducer: {
    someFeature: someSlice.reducer,
    ...
  },
});
```
## Providing the store to React components

The Redux store is defined in the component tree using its `Provider` component. The value of the Redux store (from `configureStore`) needs to be specified on the `Provider` component. The `Provider` component must be placed above the [[React Component Tree|components]] requiring access to the store:
```jsx
<Provider store={store}>
	<SomeComponent />
	<AnotherComponent />
</Provider>
```

### Accessing the store from the component
[[React Component|Components]] can access state from the Redux store using a `useSelector` hook from React Redux. A function that selects the relevant state in the store is passed into `useSelector`:
```ts
const someValue = useSelector(
	(state: RootState) => state.someFeature.someValue
)
```

## Dispatching actions to the store

React Redux also has a `useDispatch` hook that returns a `dispatch` function that can be used to dispatch actions. The action is a function from the slice created using `createSlice`:
```jsx
const dispatch = useDispatch();
return (
	<button onClick={() => dispatch(someSlice.actions.someAction())}>
		Some button
	</button>
);
```