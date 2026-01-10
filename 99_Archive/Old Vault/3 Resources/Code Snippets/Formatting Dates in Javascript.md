---
uuid: 20220802164410
created: 2022-08-02T16:44:10
alias: форматирование дат
---

# [[Formatting Dates in Javascript]]

If you want to use a standard format for a specific locale in [[JavaScript]], life is a bit easier. You can use the `Intl.DateTimeFormat` object to perform the conversion. Here are three examples that use locale strings for the US, the UK, and Japan:

```javascript
const date = new Date(2020, 11, 20, 3, 0, 0);
// Use the standard US date format
console.log(new Intl.DateTimeFormat('en-US').format(date));  // '12/20/2020'

// Use the standard UK date format
console.log(new Intl.DateTimeFormat('en-GB').format(date));  // '20/12/2020'

// Use the standard Japanese date format
console.log(new Intl.DateTimeFormat('ja-JP').format(date));  // '2020/12/20
```

All of these are date-only strings, but there are many other options you can set when you create the `Intl.DateTimeFormat()` object. Here’s just one example that adds the day of the week and month to the string, in German:

```javascript
const date = new Date(2020, 11, 20);
const formatter = new Intl.DateTimeFormat('de-DE',  { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet