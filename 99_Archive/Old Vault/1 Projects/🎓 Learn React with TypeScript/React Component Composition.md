---
created: 2023-10-18T06:20:34
aliases:
  - композиция react-компонентов
tags:
  - type/note
topic:
  - "[[React Components]]"
  - "[[Composition]]"
source: "[[Ultimate React Course]]"
---
# [[React Component Composition]]

Передавать [[React Component|компоненты]] в другие можно несколькими спобособами:
1. `{ children }`:
```js
export function NavBar({ children }) {
	return (
		<nav className="nav-bar">
			<Logo />
			{children}
		</nav>
	);
}
<NavBar>
	<Search />
	<NumResults movies={movies} />
</NavBar>
```

2. Как [[React Component|prop]]:
```js
export function Box({ element }) {
  const [isOpen1, setIsOpen1] = useState(true);

  return (
    <div className="box">
      <button className="btn-toggle" onClick={() => setIsOpen1((open) => !open)}>
        {isOpen1 ? '–' : '+'}
      </button>
      {isOpen1 && element}
    </div>
  );
}

<Box element={<MovieList movies={movies} />} />
<Box
  element={
	<>
	  <WatchedSummary watched={watched} />
	  <WatchedMovieList watched={watched} />
	</>
  }
/>
```
Последний подход реализует библиотека [[react-router]]. 

>[!note]
>Использовать `{ children }` - рекомендованный способ.

