---
uuid: 20230917145943
created: 2023-09-17T14:59:43
aliases:
  - ссылочная прозрачность
---

# [[Referential transparency]]

In [[020 Math|Math]], referential transparency is the property that lets you replace an expression with its value without changing the results of whatever you are doing. The counterpart of referential transparency is, appropriately enough, **referential opacity**. A referentially opaque function cannot guarantee that it will always produce the same result, even when called with the same arguments.

To give a simple example, let’s consider what happens with an optimizing [[Компилятор|compiler]] that performs constant folding. Suppose you have a sentence like this:
```js
const x = 1 + 2 * 3;
```
The compiler might optimize the code to the following by noting that `2*3` is a constant value: `const x = 1 + 6;`

Even better, a new round of optimization could avoid the sum altogether:
```js
const x = 7;
```
To save execution time, the compiler is taking advantage of the fact that all mathematical expressions and functions are (by definition) referentially transparent.
  
On the other hand, if the compiler cannot predict the output of a given expression, it won’t be able to optimize the code in any fashion, and the calculation will have to be done at runtime.

## Of lambdas and betas

In [[Лямбда-исчисление|lambda calculus]], if you replace the value of an expression involving a function with the calculated value for the function, then that operation is called a $β (beta)$ reduction. Note that you can only do this safely with referentially transparent functions.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Mastering JavaScript Functional Programming]]
- 🏷️ Tags::  [[Functional Programming]]