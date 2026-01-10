---
uuid: 20220719095048
created: 2022-07-19T09:50:48
alias: 
- export function
- substack pattern
---

# [[Exporting a function in CJS]]

One of the most popular [[Module definition patterns|module definition patterns]] consists of reassigning the
whole `module.exports` variable to a function. 

The **main strength** of this pattern is the fact that it allows you to **expose only a single functionality**, which provides a clear entry point for the module, making it **simpler to understand and use**; it also honors the principle of *small surface* area very well. 

```javascript
// file logger.js
module.exports = (message) => {
	console.log(`info: ${message}`)
}
```

A possible **extension** of this pattern is **using the exported function as a namespace**
for other public APIs. This is a very powerful combination because it still gives the
module the clarity of a single entry point (the main exported function) and at the
same time it allows us to expose other functionalities that have secondary or more
advanced use cases. 

```javascript
// extenstion of logger.js
module.exports.verbose = (message) => {
	console.log(`verbose: ${message}`)
}

// file main.js
const logger = require('./logger')
logger('This is an informational message')
logger.verbose('This is a verbose message')
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- source: [[NodeJS Design Patterns]]