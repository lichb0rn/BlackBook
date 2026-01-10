---
uuid: 20220720190448
created: 2022-07-20T19:04:48
alias: instance export
---

# [[Exporting and instance in CJS]]
We can leverage the caching mechanism of require() to easily define
stateful instances created from a constructor or a factory, which can be shared
across different modules.

```javascript
// file logger.js
class Logger {
	constructor (name) {
		this.count = 0
		this.name = name
	}
	log (message) {
		this.count++
		console.log('[' + this.name + '] ' + message)
	}
}
module.exports = new Logger('DEFAULT')
```

```javascript
// main.js
const logger = require('./logger')
logger.log('This is an informational message')
```

Because the module is cached, **every module** that requires the logger module will
actually **always retrieve the same instance of the object**, thus sharing its state. This
pattern is very much like creating a [[Singleton|singleton]]. However, **it does not guarantee
the uniqueness of the instance across the entire application**, as it happens in the
traditional singleton pattern. When analyzing the resolving algorithm, we have seen
that a module might be installed multiple times inside the dependency tree of an
application. This results in multiple instances of the same logical module, all running
in the context of the same [[Node.js]] application. 

One interesting detail of this pattern is that **it does not preclude the opportunity to
create new instances**, even if we are not explicitly exporting the class. In fact, we can
rely on the constructor property of the exported instance to construct a new instance
of the same type:

```javascript
const customLogger = new logger.constructor('CUSTOM')
customLogger.log('This is an informational message')
```
>[!warning]
>this technique must be used with caution or avoided altogether.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]