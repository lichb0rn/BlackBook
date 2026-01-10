---
uuid: 20220805202437
created: 2022-08-05T20:24:37
alias: перевод чисел из одного диапазона в другой
---

# [[Map a range of numbers to another range of numbers]]

```javascript
const scale = (num, in_min, in_max, out_min, out_max) => {
	return ((num - in_min) * (out_max - out_min)) / (in_max - in_min) + out_min;
};
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note