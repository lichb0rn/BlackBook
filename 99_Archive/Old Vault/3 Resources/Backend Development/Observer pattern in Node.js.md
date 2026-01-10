---
uuid: 20220802162639
created: 2022-08-02T16:26:39
alias: 
- паттерн наблюдатель в node.js 
- eventemitter
- event emitter
---

# [[Observer pattern in Node.js]]

Another important and fundamental pattern used in [[Node.js]] is the [[Observer pattern]].

## EventEmitter
The EventEmitter class allows us to register one or more functions as listeners, which will be invoked when a particular event type is fired.
![[Pasted image 20220802174234.png]]

The EventEmitter is exported from the events core module. 
```javascript
import { EventEmitter } from 'events'
const emitter = new EventEmitter()
```

The **essential methods** of the EventEmitter are as follows:
• `on(event, listener)`: This method allows us to register a new listener (a function) for the given event type (a string)
- `once(event, listener)`: This method registers a new listener, which is then removed after the event is emitted for the first time.
- `emit(event, [arg1], [...])`: This method produces a new event and provides additional arguments to be passed to the listeners.
- `removeListener(event, listener)`: This method removes a listener for the specified event type.


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note