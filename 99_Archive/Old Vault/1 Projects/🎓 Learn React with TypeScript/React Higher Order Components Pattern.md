---
created: 2023-11-10T09:32:59
aliases:
  - HOC
tags:
  - type/note
topic:
  - "[[React]]"
source: "[[Ultimate React Course]]"
---
# [[React Higher Order Components Pattern]]

Higher Order Component (HOC) - компонент, который оборачивает другой компонент, добавляя логику.

```js
function withStyles(Component) {
  return props => {
    const style = { padding: '0.2rem', margin: '1rem' }
    return <Component style={style} {...props} />
  }
}

const Button = () = <button>Click me!</button>
const Text = () => <p>Hello World!</p>

const StyledButton = withStyles(Button)
const StyledText = withStyles(Text)
```

[patterns.dev](https://www.patterns.dev/react/hoc-pattern)