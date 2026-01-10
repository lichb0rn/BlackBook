---
uuid: 20220731113152
created: 2022-07-31T11:31:52
alias: удаление пробельных символов
---

# [[Removing whitespace in Javascript]]

One common problem that thwarts the [[JavaScript]] `trim()` method is removing excess whitespace inside a string. The `replaceAll()` method can accomplish this task with relative ease using a regular expression with the `\s` character to match whitespace:

```javascript
const paddedString = 'The road is long,    with many a    winding turn.';
const trimmedString = paddedString.replaceAll(/\s\s+/g, ' ');

// trimmedString = 'The road is long, with many a winding turn.'
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 