---
uuid: 20220731113558
created: 2022-07-31T11:35:58
alias: сравнение строк
---

# [[Performing a Case-Insensitive String Comparison]]

Bulletproof approach is to use the [[JavaScript]] `String.localeCompare()` method with sensitivity set to accent, as shown here:

```javascript
const a = "hello";
const b = "HELLO";

if (a.localeCompare(b, undefined, { sensitivity: 'accent' }) === 0) {
  // We end up here, because the case-insensitive strings match.
}
```

If `localeCompare()` deems that two strings match, it returns `0`. Otherwise it returns a positive or negative integer indicating whether the compared string falls before or after the referenced string in the sort order. (Because we’re using `localeCompare()` to test for equality, the sort order isn’t important, and you can ignore it.)

To perform a case-insensitive comparison, you need to set the `sensitivity` property. There are two values that can work. If you set sensitivity to `accent`, characters that have different accents (like `a `and `á`) are treated as unequal. But if you set sensitivity to base, you’ll get a more permissive case-insensitive comparison that treats all accented letters as matches.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 