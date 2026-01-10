---
created: 2023-10-01T06:32:48
aliases:
  - lazy loading components
  - отложенная загрузка компонент
tags:
  - type/note
topic: "[[React Components]]"
source:
---
# [[React Lazy Loading]]

By default, all [React] components are bundled together and loaded when the app first loads. This is inefficient for large apps – particularly when a user does not use many components. Lazily loading React components addresses this issue because lazy components aren’t included in the initial bundle that is loaded; instead, their [[JavaScript]] is fetched and loaded when rendered.

There are two main steps to lazy loading React components. 
- First, the component must be dynamically imported as follows:
```ts
const LazyPage = lazy(() => import('./LazyPage'));
```
In the code block, `lazy` is a function from [[React]] that enables the imported component to be lazily loaded. Note that the lazy page must be a [[Named exports in ESM|default export]] – lazy loading doesn’t work with named exports.

- The second step is to render the lazy component inside React’s `Suspense` component as follows:
```jsx
<Route
	path="lazy"
	element={
		<Suspense fallback={<div>Loading...</div>}>
			<LazyPage />
		</Suspense>
	}
/>
```
