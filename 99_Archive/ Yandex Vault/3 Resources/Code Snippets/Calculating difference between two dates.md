---
uuid: 20220731113344
created: 2022-07-31T11:33:44
alias: разница между двумя датами
---

# [[Calculating difference between two dates]]

For example, if you’ve created a `getDaysSince()` function in [[JavaScript]] for calculating the difference between dates (see “Calculating the Time Elapsed Between Two Dates”), you can use it in a template literal like this:

```javascript
function getDaysSince(date) {
  const today = new Date();
  const oneDay = 24 * 60 * 60 * 1000; // hours*minutes*seconds*milliseconds
  return Math.round(Math.abs((today - date) / oneDay));
}

employeeDetail = `Our team includes ${firstName} ${lastName}. They've been a
team member since ${hireDate}! That's ${getDaysSince(hireDate)} days.`;
```


---

## 📇 Additional Metadata

- 🗂 Type:: 