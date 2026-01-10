---
uuid: 20230920152818
created: 2023-09-20T15:28:18
aliases:
  - context
---

# [[JavaScript this]]

The next special object is called `this`, which behaves differently when used inside a standard [[Функции в JavaScript|javascript function]] and an arrow function.

- *Inside a standard function*, **it is a reference to the context object that the function is operating on** — often called the ё value (when a function is called in the global scope of a web page, the this object points to window). Consider the following:

```javascript
window.color = 'red';
let o = { 
	color: 'blue'
};
function sayColor() { 
	console.log(this.color);
}
sayColor(); // 'red'
o.sayColor = sayColor; 
o.sayColor(); // 'blue'
```

The function `sayColor()` is defined globally but references the `this` object. The value of **`this` is not determined until the function is called**, so its value may not be consistent throughout the code execution. When `sayColor()` is called in the global scope, it outputs “red” because this is pointing to window, which means `this.color` evaluates to `window.color`. By assigning the function to the object `o` and then calling `o.sayColor()`, the this object points to `o`, so `this.color` evaluates to `o.color` and "blue" is displayed.

- *Inside an arrow function*, **`this` references the context in which the arrow function expression is defined**. This is demonstrated in the following example, where two different invocations of `sayColor` both reference the property of the `window` object, which is the context inside which the arrow function was initially defined:
```javascript
window.color = 'red'; 
let o = {
	color: 'blue' 
};
let sayColor = () => console.log(this.color); 
sayColor(); // 'red'
o.sayColor = sayColor; 
o.sayColor(); // 'red'
```
**This behavior is especially useful in situations where events or timeouts will invoke a function inside a callback where the invoking object is not the intended object.**


---

## 📇 Additional Metadata
- 🛠️ Status:: #📚
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Professional JavaScript for Web Developers]]
- 🏷️ Tags:: [[JavaScript]]