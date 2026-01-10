---
created: 2023-11-10T09:48:43
aliases:
  - compound pattern
tags:
  - type/note
topic:
  - "[[React]]"
  - "[[Software Design Patterns|design patterns]]"
source: "[[Ultimate React Course]]"
---
# [[React Compound Component Pattern]]

Compound pattern позволяет объединять компоненты, которые должны работать вместе (например, `select` + `option`). Для создания используется [[React Context|useContext]].

В `App.js`:
```javascript
<Counter>
	<Counter.Label>My flexible counter</Counter.Label>
	<Counter.Increase icon="+" />
	<Counter.Decrease icon="-" />
	<Counter.Count />
</Counter>
```
Мы можем конфигурировать компонент как угодно, меняя местами или удаляя его "части".

Сам компонент:
```javascript
import { createContext, useContext, useState } from "react";

const CounterContext = createContext();

function Counter({children}) {
  const [count, setCount] = useState(0);
  const increase = () =%3E setCount((c) => c + 1);
  const decrease = () => setCount((c) => c - 1);

  return <CounterContext.Provider value={{count, increase, decrease}}>
    <span>{children}</span>
  </CounterContext.Provider>;
}

function Count() {
  const {count} = useContext(CounterContext);
  return <span>{count}</span>
}

function Label({children}) {
  return <span>{children}</span>
}

function Increase({icon}) {
  const { increase } = useContext(CounterContext);
  return <button onClick={increase}>{icon}</button>
}

function Decrease({icon}) {
  const { decrease } = useContext(CounterContext);
  return <button onClick={decrease}>{icon}</button>
}

Counter.Count = Count;
Counter.Label = Label;
Counter.Increase = Increase;
Counter.Decrease = Decrease;

export default Counter;
```


[patterns.dev](https://www.patterns.dev/react/compound-pattern)
