---
uuid: 20220925150830
created: 2022-09-25T15:08:30
alias:
---

# [[Lazy Initialization in Swift]]

There are four types of variable that can be initialized lazily in [[Swift|Swift]]:

### Global variables
Global variables are automatically `lazy`. This makes sense if you ask yourself when they should be initialized. As the app launches, files and their top-level code are encountered. It would make no sense to initialize globals now, because the app isn’t even running yet. Thus global initialization must be postponed to some moment that does make sense. Therefore, a global variable’s initialization doesn’t happen until other code first refers to that global. Under the hood, this behavior is implemented in such a way as to make initialization both singular (it can happen only once) and thread-safe.

### Static properties
Static properties are automatically lazy. They behave exactly like global variables, and for basically the same reason. (There are no stored class properties in Swift, so class properties can’t be initialized and thus can’t have lazy initialization.)

### Instance properties
An instance property is not lazy by default, but it may be made lazy by marking its declaration with the keyword lazy. This property must be declared with var, not let.

### Local variables
New in Swift 5.5, a local variable can be declared with lazy var.


## Lazy Initialization of Instance Properties

Aside from the efficiency benefits of a laziness, a lazy initializer can do things that a normal initializer can’t. In particular, a **lazy initializer can refer to the instance**. A normal initializer can’t do that, because the instance doesn’t yet exist at the time that a normal initializer would need to run (we’re in the middle of creating the instance, so it isn’t ready yet). A lazy initializer, by contrast, is guaranteed not to run until some time after the instance has fully come into existence, so referring to the instance is fine.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[iOS 15 Programming Fundamentals with Swift]]