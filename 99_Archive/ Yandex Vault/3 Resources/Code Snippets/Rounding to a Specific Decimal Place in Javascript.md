---
uuid: 20220802163724
created: 2022-08-02T16:37:24
alias: округление в javascript
---

# [[Rounding to a Specific Decimal Place in Javascript]]

Oddly enough, in [[JavaScript]] the ``round()`` method doesn’t take an argument that lets you specify a number of decimal places to keep. If you want a different degree of precision, it’s up to you to multiply your number by the appropriate power of 10, round it, and then divide it by the same power of 10 after rounding. Here’s the general formula for this operation:

```javascript
const numberToRound = fractionalNumber * (10**numberOfDecimalPlaces);
let roundedNumber = Math.round(numberToRound);
roundedNumber = roundedNumber / (10**numberOfDecimalPlaces);
```

For example, if you want to round to two decimal places, the code becomes this:

```javascript
const fractionalNumber = 19.48938;
const numberToRound = fractionalNumber * (10**2);
let roundedNumber = Math.round(numberToRound);
roundedNumber = roundedNumber / (10**2);
// Now roundedNumber is 19.49
```  

If you want to round left of decimal place (for example, to the nearest tens, hundreds, and so on), just use a negative number for `numberOfDecimalPlaces`. For example, `–1` rounds to the nearest `10`, `–2` rounds to the nearest `100`, and so on.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- 🏷️ Tags:: [[JavaScript]]