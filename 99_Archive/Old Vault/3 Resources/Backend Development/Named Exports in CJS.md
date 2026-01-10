---
uuid: 20220719094502
created: 2022-07-19T09:45:02
alias: именованные экспорты
---

# [[Named Exports in CJS]]

The most basic method for exposing a public API is using named exports, which
involves assigning the values we want to make public to properties of the object
referenced by `exports` (or `module.exports`).  In this way, the resulting exported
object becomes a container or namespace for a set of related functionalities.

```javascript
// file logger.js
exports.info = (message) => {
	console.log(`info: ${message}`)
}

exports.verbose = (message) => {
	console.log(`verbose: ${message}`)
}

// file main.js
const logger = require('./logger')
logger.info('This is an informational message')
logger.verbose('This is a verbose message')
```

Most of the [[Node.js]] core modules use this [[Module definition patterns|pattern]]. However, the [[CommonJS]]
specification only allows the use of the exports variable to expose public members.
Therefore, the named exports pattern is the only one that is really compatible with
the [[CommonJS]] specification. 


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]