---
uuid: 20230917151045
created: 2023-09-17T15:10:45
aliases:
  - javascript function
  - caller
  - new.target
---

# [[Функции в JavaScript]]

## Способы определения функции
• A named **function declaration**: `function first(...) {...};`
• An *anonymous function expression*: `var second = function(...) {...};`
• A **named function expression**: `var third = function someName(...) {...};`
• An **immediately-invoked expression**: `var fourth = (function() { ...; return function(...) {...}; })();`
• A **function constructor**: `var fifth = new Function(...);`
• An **arrow function**: `var sixth = (...) => {...};`

The first definition, `function first(...) {...}`, a standalone declaration starting with the function keyword, is probably the most used in [[JavaScript]] and defines a function named `first` (that is, `first.name==="first"`). Because of [[JavaScript  Hoisting|hoisting]], this function will be accessible everywhere in the [[JavaScript scope|scope]] where it’s defined

The `second = function(...) {...}` definition, which assigns a function to a variable, also produces a function, but an anonymous (that is, not named) one. However, many JavaScript engines can deduce what the name should be and will then set `second.name === "second"`. (Look at the following code, which shows a case where the anonymous function has no name assigned.) Since the assignment isn’t hoisted, the function will only be accessible after the assignment has been executed.

The third definition, `third = function someName(...) {...}`, is the same as the second, except that the function now has its own name: `third.name === "someName"`. The name of a function is relevant when you want to call it and is needed for recursive calls

The fourth definition, `fourth = (function() { ...; return function(...) {...}; })()`, with an [[Immediately Invoked Function Expression|IIFE]], lets you use a closure.  An inner function can use variables or other functions, defined in its outer function, in a private, encapsulated way. 

The fifth definition, `fifth = new Function(...)`, isn’t safe and you shouldn’t use it! You pass the names of the arguments first, then the actual function body as a string, and the equivalent of `eval()` is used to create the function.

## Arrow functions – the modern way

^c853c7

Even if arrow functions work in pretty much the same way as the other functions, there are some crucial differences between them and the usual ones: arrow functions can implicitly return a value even with no return statement present; the value of this (the context for the function) is not bound; there is no arguments object; they cannot be used as constructors; they do not have a prototype property; and they cannot be used as generators because they don’t allow the yield keyword.

## caller
[[ECMAScript]] also formalizes an additional property on a function object: `caller`. 
This property **contains a reference to the function that called this function or null if the function was called from the global scope**. For example:
```javascript
function outer() { 
	inner();
}

function inner() {
	console.log(inner.caller); 
}
outer();
```
This code displays an alert with the source text of the `outer()` function. Because `outer()` calls `inner()`, `inner.caller` points back to `outer()`. 

For looser coupling, you can also access the same information via `arguments.callee.caller`:
```javascript
function outer() { 
	inner();
}
function inner() {
	console.log(arguments.callee.caller);
}
outer();
```

## new.target

Functions have always been able to behave as both a [[JavaScript Class|constructor]] to instantiate a new [[JavaScript Object|object]] and as a normal callable function. To address this, [[ECMAScript]] supports the ability to determine if a function was invoked with the `new` keyword using `new.target`. Suppose we have this simple function:
```javascript
function foo() {}
```
If this function is called using `foo()`, `new.target` will be undefined. 
If this function is called using `new foo`, `new.target` will reference the constructor or function.
```javascript
function King() {
	if (!new.target) {
		throw 'King must be instantiated using "new"' 
	}
	console.log('King instantiated using "new"'; 
}
```

---

## 📇 Additional Metadata
- 🛠️ Status:: #📚
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Mastering JavaScript Functional Programming]]
- 🏷️ Tags:: [[JavaScript]], [[Функция|function]]