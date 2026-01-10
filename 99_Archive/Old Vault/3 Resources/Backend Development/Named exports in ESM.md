---
uuid: 20220720192521
created: 2022-07-20T19:25:21
alias: modules in javascript
---

# [[Exports in ESM]]
- exporting:
```javascript
// logger.js

// exports a function as `log`
export function log (message) {
	console.log(message)
}

// exports a constant as `DEFAULT_LEVEL`
export const DEFAULT_LEVEL = 'info'

// exports an object as `LEVELS`
export const LEVELS = {
	error: 0,
	debug: 1,
	warn: 2,
	data: 3,
	info: 4,
	verbose: 5
}
// exports a class as `Logger`
export class Logger {
	constructor (name) {
		this.name = name
	}
	log (message) {
	console.log(`[${this.name}] ${message}`)
	}
}
```

- importing:
```javascript
import * as loggerModule from './logger.js'
console.log(loggerModule)

```
In this example, we are using the `*` syntax (also called **namespace import**) to import
all the members of the module and assign them to the local `loggerModule` variable.

If we are using a large module, most often we don't want to import all of its functionality, but only one or few entities from it:
```javascript
import { log } from './logger.js'
log('Hello World')

// or

import { log, Logger } from './logger.js'
log('Hello World')
const logger = new Logger('DEFAULT')
logger.log('Hello world')

```

## Default exports
```javascript
// logger.js
export default class Logger {
	constructor (name) {
		this.name = name
	}
	log (message) {
		console.log(`[${this.name}] ${message}`)
	}
}
```

In this case, the name `Logger` is ignored, and the entity exported is registered under the name `default`. This exported name is handled in a special way, and it can be imported as follows:

```javascript
import MyLogger from './logger.js'
const logger = new MyLogger('info')
logger.log('Hello World')
```

The difference with named ESM imports is that here, since the `default` export is **considered unnamed**, **we can import it and at the same time assign it a local name of
our choice**. In this example, we can replace `MyLogger` with anything else that makes sense in our context. 

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]