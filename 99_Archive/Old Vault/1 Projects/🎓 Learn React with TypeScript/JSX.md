---
created: 2023-09-27T09:30:51
aliases:
  - jsx
  - javascript xml
tags:
  - type/note
topic: "[[React]]"
source:
---
# [[JSX]]

JSX is the syntax we use in a [[React Component]] to define what the component should display:
```javascript
function App() {
	return (
		<div className="App">
			<Alert type="information" heading="Success">
				Hello world!
			</Alert>
		</div>
	)
}
```
You can see that JSX looks a bit like [[064 HTML and CSS|html]]. However, it isn’t HTML because an HTML `div` element doesn’t contain a `className` attribute, and there is no such element name as `Alert`. The JSX is also embedded directly within a [[Функции в JavaScript|javascript function]], which is a little strange because a script element is normally used to place [[JavaScript]] inside HTML.

JSX is a [[JavaScript]] **syntax extension**. This means that it doesn’t execute directly in the browser – it needs to be **transpiled** to JavaScript first. A popular tool that can transpile JSX is called [[Babel]].

### Пример
Допустим есть такой jsx-код:
```jsx
const title="Oh no!";

<div className={title}>
	<span>{title ? title : "Important"}</span>
</div>
```
Он будет [[Transpilation|транспилирован]] в:
```javascript
const title = "Oh no!";
/*#__PURE__*/React.createElement("div", {
  className: title
}, /*#__PURE__*/React.createElement("span", null, title ? title : "Important"));
```

## Fragments
The empty JSX elements, `<>` and `</>`, are **React fragments**. [[React]] fragments are not added to the [[DOM]] and are used as a workaround to React components only being able to return a single element, so they are a way of returning multiple elements in a React component that keeps React happy.
```typescript
import { Outlet } from 'react-router-dom';
import { Header } from './Header';

function App() {
  return (
    <>
      <Header />
      <Outlet />
    </>
  );
}
export default App;
```

