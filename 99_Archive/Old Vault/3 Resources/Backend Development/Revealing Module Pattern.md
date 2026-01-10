---
uuid: 20220717165832
created: 2022-07-17T16:58:32
alias: revealing module pattern
---

# [[Revealing Module Pattern]]

In short, relying on the global scope is a very risky business, especially as
your application grows and you have to rely more and more on functionality
implemented by other individuals.

A popular technique to solve this class of problems in [[JavaScript]] is called the revealing module pattern, and it looks like this:
```javascript
const myModule = (() => {
	const privateFoo = () => {}
	const privateBar = []

	const exported = {
		publicFoo: () => {},
		publicBar: () => {}
	}
	return exported
})() // once the parenthesis here are parsed, the function
// will be invoked

console.log(myModule)
console.log(myModule.privateFoo, myModule.privateBar)
```

This pattern leverages a self-invoking function. This type of function is sometimes
also referred to as [[Immediately Invoked Function Expression]] (IIFE) and it is used
to create a private scope, exporting only the parts that are meant to be public

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note