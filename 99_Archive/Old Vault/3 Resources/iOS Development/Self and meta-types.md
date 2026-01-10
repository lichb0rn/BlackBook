---
uuid: 20221105080929
created: 2022-11-05T08:09:29
alias:
- Self
- meta-type
tags: 
---

# [[Self and meta-types]]

in [[Swift|swift]] `self` is usually a reference to the object whose scope you’re currently in. 

If you use self inside an instance method of a `User` struct, self will be that instance of that struct. So far, that’s pretty straightforward. 

However, when you’re in a class method of a [[Swift Class|class]], self can’t be a reference to an instance because there is no instance: You’re in the class itself.

```swift
class Networker {
  class func whoAmI() {
    print(self)
  }
}
Networker.whoAmI() // "Networker"
```

In class and static methods, ``self`` has the value of the current type, not an instance. 

It makes sense when you think about it: Static and class methods exist on the type, not an instance.

Just like Int holds all integer values, `Int`.Type holds all Int type values. These types that hold other types are called meta-types.

```swift
class WebsocketNetworker: Networker {
  class func whoAmI() -> Networker.Type {
    return self
  }
}
let type: Networker.Type = WebsocketNetworker.whoAmI()
print(type)
```

In the example above, you declare a meta-type variable called type. 
The meta-type can hold not only the `Networker` type itself but also all of its subclasses, such as `WebsocketNetworker`. 

In the case of [[Swift Protocol|protocols]], a meta-type of a protocol (`YourProtocol.Type`) can hold the protocol type as well as all concrete types conforming to that protocol.

`Self` is always an alias to the concrete type of the scope it appears in. Concrete is emphasized because `Self` will always be a concrete type, even if it’s used inside a protocol method.
```swift
extension Request {
  func whoAmI() {
    print(Self.self)
  }
}
TextRequest().whoAmI() // "TextRequest"
```
 
`Self` is useful when you want to return the current concrete type from a protocol method or use it as an initializer inside a static method when creating factory methods.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]