---
uuid: 20220720191020
created: 2022-07-20T19:10:20
alias: monkey patching
---

# [[Modifying other modules or the global scope in CJS]]

>[!warning]
>these are in general considered bad practices, but since this pattern can be useful and safe under some circumstances (for example, for **testing**) and it's sometimes used in real-life projects

A module can even export nothing. This can seem a bit out of place; however, we should not forget that a **module can modify the global scope and any object in it**, including other modules in the cache. 

We said that a module can modify other modules or objects in the global scope; well, this is called **monkey patching**. It generally refers to the practice of modifying the existing objects at runtime to change or extend their behavior or to apply temporary fixes.

```javascript
// file patcher.js

// ./logger is another module
require('./logger').customMessage = function () {
	console.log('This is a new functionality')
}
```
```javascript
// file main.js
require('./patcher')
const logger = require('./logger')
logger.customMessage()
```

The main concern is that having a module that modifies the global namespace or other modules is an operation with ***side effects***. In other words, it affects the state of entities outside their scope, which can have consequences that aren't easily predictable, especially when
multiple modules interact with the same entities. Imagine having two different modules trying to set the same global variable, or modifying the same property of the same module. The effects can be unpredictable (which module wins?), but most importantly it would have repercussions on the entire application.

>[!note] используется для mock'ов http
>https://github.com/nock/nock

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]