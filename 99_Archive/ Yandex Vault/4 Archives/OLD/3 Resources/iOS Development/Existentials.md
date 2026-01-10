---
uuid: 20220916164630
created: 2022-09-16T16:46:30
alias:
---

# [[Existentials]]

Strictly speaking, [[Swift Protocol|protocols]] cannot be used as concrete types in [[Swift|Swift]]; they can only be used to constrain [[Swift Generics|generic]] parameters. Surprisingly though, the following code compiles

```swift
let context: DrawingContext = SVG()
```

When we’re using a protocol like a concrete type, the compiler creates a wrapper type for the protocol, called an **existential**, behind the scenes. `let context: DrawingContext` is essentially [[Syntactic Sugar|syntactic sugar]] for something like `let context: Any<DrawingContext>`.

Although this syntax doesn’t exist, the compiler creates an ``Any`` box (which is 32 bytes large), and adds an 8-byte [[Protocol Witness|protocol witness]] for each protocol. We can verify it for the example above like this:

```swift
MemoryLayout<Any>.size // 32 
MemoryLayout<DrawingContext>.size // 40
```

**This box around the protocol(s) is also called an existential container.** The **compiler has to create these containers, because it has to know the size of the type at compile time**. Since different types with different sizes can conform to a protocol (e.g. [[Swift Class|classes]], which all have the size of a pointer, and [[Swift Structures|structs]] or [[Swift Enumeration|enums]], which have different sizes depending on their contents), wrapping the protocol(s) up in an existential container creates a type with constant size for the compiler to lay values out in memory.

Sometimes existentials can be used interchangeably with constrained generic parameters. Consider the following two functions:

```swift
func encode1(x: Encodable) { }
func encode2<E: Encodable>(x: E) { }
```

While we can call both functions with any type that conforms to [[Encodable]], they are perhaps surprisingly not equivalent. In the case of `encode1`, the compiler will wrap the parameter in an [[Encodable]] existential container. This **wrapping costs some performance and possibly requires an extra memory allocation call if the wrapped value is too big** to fit into the existential directly. Perhaps more importantly, **the existential prevents further optimizations because all method calls on the wrapped value have to go through the existential’s witness table**.

**For the generic function**, on the other hand, the **compiler can generate specialized versions for some or all of the types `encode2` is called with**. These specializations achieve the same performance as manually overloading the function for every concrete type we want to pass in does. The downsides compared to the version taking an existential are longer compile times and a larger binary size.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Advanced Swift]]