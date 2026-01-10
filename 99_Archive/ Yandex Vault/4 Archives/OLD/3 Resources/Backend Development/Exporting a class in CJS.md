---
uuid: 20220720185838
created: 2022-07-20T18:58:38
alias: export class
---

# [[Exporting a class in CJS]]
Exporting a class still provides a single entry point for the module, but compared
to the [[Exporting a function in CJS]], it exposes a lot more of the module internals. On the other hand, it allows much more power when it comes to extending its functionality

```javascript
class Logger {
	constructor (name) {
		this.name = name
	}
	log (message) {
		console.log(`[${this.name}] ${message}`)
	}
	info (message) {
		this.log(`info: ${message}`)
	}
	verbose (message) {
		this.log(`verbose: ${message}`)
	}
}

module.exports = Logger
```

```javascript
// file main.js
const Logger = require('./logger')
const dbLogger = new Logger('DB')
dbLogger.info('This is an informational message')
const accessLogger = new Logger('ACCESS')
accessLogger.verbose('This is a verbose message')
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]