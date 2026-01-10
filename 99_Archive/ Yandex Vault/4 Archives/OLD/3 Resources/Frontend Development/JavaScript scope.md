---
created: 2023-09-23T12:02:11
aliases:
  - область видимости
  - scope
tags:
  - type/note
topic: "[[Closure]]"
source: "[[Professional JavaScript for Web Developers]]"
---
# [[JavaScript scope]]

When a [[Функции в JavaScript|javascript function]] is called, an **execution context is created, and its scope chain is created**. The **activation object** for the function is initialized with values for arguments and any named arguments. The outer function’s activation object is the second object in the scope chain. This process continues for all containing functions until the scope chain terminates with the global execution context.

As the function executes, variables are looked up in the scope chain for the reading and writing of values. Consider the following:  
```javascript
function compare(value1, value2) { 
	if (value1 < value2) {
		return -1;
	} else if (value1> value2) {
		return 1
	} else {
		return 0
	} 
}
let result = compare(5, 10)
```
This code defines a function named `compare()` that is called in the **global execution context**. When `compare()` is called for the first time, a new activation object is created that contains arguments, `value1`, and `value2`. The global execution context’s variable object is next in the `compare()` execution context’s scope chain, which contains [[JavaScript this|this]], `result`, and `compare`.

![[Pasted image 20230923120541.png]]

Behind the scenes, an object represents the variables in each execution context. The **global context’s variable object always exists**, whereas local context variable objects, such as the one for `compare()`, exist only while the function is being executed. 

- When `compare()` is defined, its **scope chain** is created, preloaded with the global variable object, and saved to the internal [[Scope]] property. 
- When the function is called, an execution context is created and its scope chain is built up by copying the objects in the function’s `[[Scope]]` property. 
- After that, an activation object (which also acts as a variable object) is created and pushed to the front of the context’s scope chain.

In this example, that means the `compare()` function’s execution context has two variable objects in its scope chain: the local activation object and the global variable object. Note that the **scope chain is essentially a list of pointers to variable objects and does not physically contain the objects**.

Whenever a variable is accessed inside a function, the scope chain is searched for a variable with the given name. Once the function has completed, the local activation object is destroyed, leaving only the global scope in memory. Closures, however, behave differently. **A function that is defined inside another function adds the containing function’s activation object into its scope chain.**

```javascript
function createComparisonFunction(propertyName) { 
	return function(object1, object2) {
		let value1 = object1[propertyName]; 
		let value2 = object2[propertyName];
		
		if (value1 < value2) { 
			return -1;
		} else if (value1 > value2) { 
			return 1;
		} else { 
			return 0;
		} 
	};
}
let compare = createComparisonFunction('name');
let result = compare({ name: 'Alice' }, { name: 'Matt' });
```

So, in `createComparisonFunction()`, the anonymous function’s scope chain **actually contains a reference to the activation object** for `createComparisonFunction()`. 
Figure 10.2 illustrates this relationship when the following code is executed:
![[Pasted image 20230923122049.png]]

When the anonymous function is returned from `createComparisonFunction()`, its scope chain has been initialized to contain the activation object from `createComparisonFunction()` and the global variable object. This gives the anonymous function access to all of the variables from `createComparisonFunction()`. 

Another interesting side effect is that the activation object from `createComparisonFunction()` cannot be destroyed once the function finishes executing, because a reference still exists in the anonymous function’s scope chain.

>[!note]
>Because closures carry with them the containing function’s scope, they **take up more memory than other functions**. Overuse of closures **can lead to excess memory consumption**, so it’s recommended you use them only when absolutely necessary. Optimizing [[JavaScript]] engines, such as [[JavaScript V8|V8]], make attempts to reclaim memory that is trapped because of closures, but it’s still recommended to be careful when using closures.