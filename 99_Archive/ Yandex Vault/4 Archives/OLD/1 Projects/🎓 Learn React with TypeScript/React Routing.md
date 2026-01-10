---
created: 2023-09-30T13:22:34
aliases:
  - routing in react
tags:
  - type/note
topic: "[[React]]"
source: "[[Learn React with TypeScript]]"
---
# [[React Routing]]

React Router is a routing library for [[React]] apps. A router is responsible for selecting what to show in the app for a requested path.

## Installing React Router

React Router is in a package called `react-router-dom`. Install this in the project using the following command in the terminal:

```bash
npm i react-router-dom
```

## Routing

A router in React Router is a component that tracks the browser’s URL and performs navigation. Several routers are available in React Router, and the one recommended for web applications is called a browser router. As its name suggests, the `createBrowserRouter` function creates a browser router.

`createBrowserRouter` requires an argument containing all the routes in the application. A route contains a path and what component to render when the app’s browser address matches that path. The following code snippet creates a router with two routes:
```typescript
const router = createBrowserRouter([
  {
    path: 'some-page',
    element: <SomePage />,
  },
  {
    path: 'another-page',
    element: <AnotherPage />,
  }
]);
```
The router returned by `createBrowserRouter` is passed to a `RouterProvider` component and placed high up in the [[React]] component tree, as shown here:
```typescript
const root = ReactDOM.createRoot(
  document.getElementById('root') as HTMLElement
);

root.render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```
