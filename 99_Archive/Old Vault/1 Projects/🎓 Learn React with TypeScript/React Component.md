---
created: 2023-09-27T10:47:57
aliases:
  - react component
  - props
  - react component state
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Component]]

>[!important]
>A React component name must start with a capital letter. If a component name starts with a lowercase letter, it is treated as a DOM element and won’t render properly.

Пример компонента:
```javascript
function Alert() {
	return (
		<div>
			<span role="img" aria-label="Warnign">
				⚠️
			</span>
			<span>Oh no!</span>
		</div>
	);
}
```

Тоже самое, но через [[Функции в JavaScript#^c853c7|стрелочные функции]]:
```javascript
const Alert = () => {
	return ( ... );
}
```
>[!note]
>There aren’t any significant differences between arrow functions and normal functions in the context of React function components. So, it is down to personal preference which one you choose.

## props
`props` is an optional parameter that is passed into a React component. This parameter is an object containing the properties of our choice. The following code snippet shows a props parameter in a `ContactDetails` component:
```javascript
function ContactDetails(props) {
	...
	// props.name
	// props.email
}
```
Props are passed into a component in [[JSX]] as attributes. The prop names must match what is defined in the component:
```jsx
<ContactDetails name="Fred" email="fred@mail.com" />
```

## state
The component state is a special variable containing information about the component’s current situation. For example, a component may be in a loading state or an error state.

State is a key part of making a component interactive. When a user interacts with a component, the component’s output may need to change. For example, clicking on a component may need to make an element in the component invisible. A **change to a component state causes the component to refresh**, more often referred to as **re-rendering**. So, a user could click on a component causing a state change, resulting in an element in the component becoming invisible.

State is defined using a `useState` function from [[React]]. The `useState` function is one of [[React Hooks|React’s hooks]]. 

Syntax:
```javascript
const [state, setState] = useState(initialValue);
```
- The initial state value is passed into `useState`. If no value is passed, it will initially be [[TypeScript null types|undefined]].
- `useState` returns a [[TypeScript tuples|typescript tuple]] containing the current state value and a function to update the state value. The tuple is destructured in the preceding code snippet.
- The `state` variable name is state in the preceding code snippet, but we can choose any meaningful name.
- We can also choose the state **setter function name**, but it is common practice to use the same name as the state variable preceded by set.
- Multiple states can be defined by defining multiple instances of `useState`. For example, here are definitions for loading and error states:
```javascript
const [loading, setLoading] = useState(true);
const [error, setError] = useState();
```

