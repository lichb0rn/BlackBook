---
uuid: 20220718093727
created: 2022-07-18T09:37:27
alias: алгоритм разрешения зависимостей commonjs
---

# [[CommonJS Dependency Management]]

## Resolving Algorithm

The resolving algorithm can be divided into the following three major branches:
• **File modules**: If `moduleName` starts with `/`, it is already considered an absolute path to the module and it's returned as it is. If it starts with `./`, then `moduleName` is considered a relative path, which is calculated starting from the directory of the requiring module.

• **Core modules**: If `moduleName` is not prefixed with `/` or `./`, the algorithm will
first try to search within the core [[Node.js]] modules.

• **Package modules**: If no core module is found matching `moduleName`, then
the search continues by looking for a matching module in the first `node_modules` directory that is found navigating up in the directory structure starting from the requiring module. The algorithm continues to search for a match by looking into the next `node_modules `directory up in the directory tree, until it reaches the root of the filesystem.

The `node_modules` directory is actually where the package managers install the
dependencies of each package. 

```
myApp
├── foo.js
└── node_modules
	├── depA
	│ └── index.js
	├── depB
	│ ├── bar.js
	│ └── node_modules
	│ └── depA
		│ └── index.js
	└── depC
		├── foobar.js
		└── node_modules
			└── depA
				└── index.js
```

In the previous example, `myApp`, `depB`, and `depC` all depend on `depA`. 
However, they all have their own private version of the dependency! Following the rules of the
resolving algorithm, using require('`depA`') will load a different file depending on the module that requires it, for example:
• Calling `require('depA')` from `/myApp/foo.js` will load `/myApp/node_modules/depA/index.js`.
	
• Calling `require('depA')` from` /myApp/node_modules/depB/bar.js` will load
`/myApp/node_modules/depB/node_modules/depA/index.js`

• Calling `require('depA')` from` /myApp/node_modules/depC/foobar.js` will
load `/myApp/node_modules/depC/node_modules/depA/index.js`


## The module cache
Each module is only loaded and evaluated the first time it is required, since any
subsequent call of `require()` will simply return the cached version. 

The module cache is exposed via the `require.cache` variable, so it is possible to
directly access it if needed. A common use case is to invalidate any cached module
by deleting the relative key in the require.cache variable, a practice that can be
useful during testing but very dangerous if applied in normal circumstances.

## Circular dependencies
But let's walk together through an example to see how [[CommonJS]] behaves when
dealing with circular dependencies. Let's suppose we have the scenario represented
![[Pasted image 20220718101253.png]]

A module called `main.js` requires `a.js` and `b.js`. In turn, `a.js `requires `b.js`. But
`b.js` relies on `a.js` as well! 

It's obvious that we have a **circular dependency** here as module `a.js` requires module `b.js` and module `b.js` requires module `a.js`. Let's have a look at the code of these two modules:
- Module` a.js`:
```javascript
exports.loaded = false
const b = require('./b')
module.exports = {
	b,
	loaded: true // overrides the previous export
}
```

- Module `b.js`:
```javascript
exports.loaded = false
const a = require('./a')
module.exports = {
	a,
	loaded: true
}
```

 - Now, let's see how these modules are required by `main.js`:
```javascript
const a = require('./a')
const b = require('./b')
console.log('a -%3E', JSON.stringify(a, null, 2))
console.log('b ->', JSON.stringify(b, null, 2))
```

Output:
```javascript
a -> {
	"b": {
		"a": {
			"loaded": false
		},
		"loaded": true
	},
	"loaded": true
}

b -> {
	"a": {
		"loaded": false
	},
	"loaded": true
}
```

This result reveals the **caveats** of circular dependencies with CommonJS, that is, **different parts of our application will have a different view** of what is exported by module `a.js` and module `b.js`, **depending on the order** in which those dependencies are loaded. 

While both the modules are completely initialized as soon as they are required from the module `main.js`, the `a.js` module **will be incomplete** when it is loaded from `b.js`. In  particular, its **state will be the one that it reached the moment** `b.js` was required

The steps are as follows:
1. The processing starts in `main.js`, which immediately requires `a.js`
2. The first thing that module `a.js` does is set an exported value called loaded
to `false`
3. At this point, module `a.js` requires module `b.js`
4. Like `a.js`, the first thing that module `b.js` does is set an exported value
called loaded to `false`
5. Now, `b.js` requires `a.js` (**cycle**)
6. Since `a.js` has already been traversed, its currently exported value
is immediately copied into the scope of module `b.js`
7. Module `b.js` finally changes the loaded value to `true`
8. Now that `b.js` has been fully executed, the control returns to `a.js`, which
now holds a copy of the current state of module `b.js` in its own scope
9. The last step of module` a.js` is to set its loaded value to `true`
10. Module `a.js` is now completely executed and the control returns to `main.js`,
which now has a copy of the current state of module `a.js` in its internal scope
11. `main.js` requires `b.js`, which is immediately **loaded from cache**
12. The current state of module `b.js` is copied into the scope of module `main.js`
where we can finally see the complete picture of what the state of every module is

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]