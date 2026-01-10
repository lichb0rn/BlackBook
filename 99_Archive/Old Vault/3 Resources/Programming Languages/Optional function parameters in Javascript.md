---
uuid: 20220805174409
created: 2022-08-05T17:44:09
alias: опциональные параметры функций в javascript
---

# [[Optional function parameters in Javascript]]

Предположим, нам нужно передавать опциональные параметры в функцию. Это можно удобно сделать с помощью создания [[Javascript Objects|объекта]]:

```javascript
someFunction(arg1, arg2, {optionalArg1: val1, optionalArg2: val2}) {}
```

В самой функции можно использовать [[JavaScript Destructuring|распаковку]]:

```javascript
function dateDifferenceInSeconds(
 newerDate, olderDate, {discardTime, discardYears, precision} = {}) {
  if (discardTime) {
    newerDate = newerDate.setHours(0,0,0,0);
    olderDate = newerDate.setHours(0,0,0,0);
  }
  if (discardYears) {
    newerDate.setYear(0);
    olderDate.setYear(0);
  }

  const differenceInSeconds = (newerDate.getTime() - olderDate.getTime())/1000;
  return differenceInSeconds.toFixed(precision);
}

// Compare the current date to an older date
const newDate = new Date();
const oldDate = new Date(2010, 1, 10);

// Call the function without an object literal
let difference = dateDifferenceInSeconds(newDate, oldDate);
console.log(difference);   // Shows something like 354378086

// Call the function with an object literal, and specify two properties
difference = dateDifferenceInSeconds(
 newDate, oldDate, {discardYears:true, precision:2});
console.log(difference);   // Shows something like 7226485.90
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[JavaScript Cookbook]]
- 🏷️ Tags:: [[JavaScript]]