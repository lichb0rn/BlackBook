---
created: 2023-09-30T07:20:04
aliases:
  - react rendering
tags:
  - type/note
topic: "[[React]]"
source: "[[Learn React with TypeScript]]"
---
# [[React rendering]]

## When a component is re-rendered
A [[React Component|component]] re-renders when its state changes. Consider the following component:

```typescript
export function SomeComponent() {
  const [someState, setSomeState] = useState('something');
  return (
    <div>
      <ChildComponent />
      <AnotherChildComponent something={someState} />
      <button
        onClick={() => setSomeState('Something else')}
      ></button>
    </div>
  );
}
```
When `someState` changes, `SomeComponent` will re-render – for example, when the button is clicked. In addition, `ChildComponent` and `AnotherChildComponent` will re-render when `someState` changes. This is because a component is re-rendered when its parent is re-rendered.

It may seem like this re-rendering behavior will cause performance problems – particularly when a component is rendered near the top of a large component tree. However, it rarely does cause performance issues. This is because the **[[DOM]] will only be updated after a re-render if the virtual DOM changes**, and updating the DOM is the slow part of the process. In the preceding example, the DOM for `ChildComponent` won’t be updated when `SomeComponent` is re-rendered if the definition of `ChildComponent` is as follows:

```typescript
export function ChildComponent() {
  return <span>A child component</span>;
}
```

The DOM for `ChildComponent` won’t be updated during a re-render because the [[React virtual DOM|virtual DOM]] will be unchanged.

While this re-rendering behavior generally doesn’t cause performance problems, it can cause performance issues if a computationally expensive component is frequently re-rendered or a component with a slow side effect is frequently re-rendered. For example, we would want to avoid unnecessary re-renders in components with a side effect that fetches data.

There is a function called `memo`in [[React]] that can be used to prevent unnecessary re-renders. The memo function can be applied as follows to `ChildComponent` to prevent unnecessary re-renders:
```typescript
export const ChildComponent = memo(() => {
	return <span>A child component</span>;
});
```
The `memo` function wraps the component and memoizes the result for a given set of [[React Component#props|props]]. The memoized function is then used during a re-render if the props are the same. Note that the preceding code snippet uses arrow function syntax so that the component can be a named export.

## Фазы

- **Render triggered**
	initial render
	[[React Component|state]] update
- **Render phase**
	На этом этапе [[React]] определяет то, что нужно перерисовать
- **Commit phase**
	Тут происходит изменение [[DOM]]
- **Browser Paint*
![[Pasted image 20231018105225.png]]

### Diffing
