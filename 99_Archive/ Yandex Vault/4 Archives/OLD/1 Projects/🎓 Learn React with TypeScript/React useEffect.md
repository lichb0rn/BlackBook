---
created: 2023-09-29T06:27:10
aliases:
  - useEffect
tags:
  - type/note
topic:
  - "[[React Components]]"
source: "[[Learn React with TypeScript]]"
---
# [[React useEffect]]

The effect Hook is used for component side effects. A component side effect is something executed outside the scope of the component such as a web service request. The effect Hook is defined using the `useEffect` function from [[React]]. `useEffect` contains two parameters: 
- A function that executes the effect; at a minimum, this function runs each time the component is rendered
- An optional array of dependencies that cause the effect function to rerun when changed

```ts
function SomeComponent() {
	function someEffect() {
		console.log('Effect');
	}
	useEffect(someEffect);
	return ...
}
	
function SomeOtherComponent({ search }) {
	useEffect(() => {
		console.log('Effect dependent on a search prop', search);
	}, [search]);
	return ...
}
```
## Effect cleanup

An effect can return a function that performs cleanup logic when the component is unmounted. Cleanup logic ensures nothing is left that could cause a memory leak.
```ts
function ExampleComponent({ onClickAnywhere }) {
	useEffect(() => {
		function handleClick() {
			onClickAnywhere();
		}
		document.addEventListener('click', handleClick);
		return function cleanup() {
			document.removeEventListener('click', handleClick);
		}
	}
	return ...
}
```

## Использование useEffect для синхронизации
`useEffect()` можно использовать для синхронизации компонент:
```js
// Синхронизируем карту, если поменялись координаты
useEffect(() => {
	if (mapLat && mapLng) setMapPosition([mapLat, mapLng]);
	}, 
[mapLat, mapLng]);

// Синхронизируем переменные
useEffect(() => {
	if (geolocationPosition) 
		setMapPosition([geolocationPosition.lat, geolocationPosition.lng]);
	}, 
[geolocationPosition]);
```
