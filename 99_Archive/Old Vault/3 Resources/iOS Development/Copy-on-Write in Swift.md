---
uuid: 20220905202630
created: 2022-09-05T20:26:30
alias:
- copy-on-write in Swift
- copy on change in Swift
- mutating struct
- mutating value type 
- копирование при записи в Swift
- копирование при изменении в Swift
---

# [[Copy-on-Write in Swift]]

[[Swift Structures|Структуры]] в [[Swift|swift]] обладают [[Value Semantics|value semantics]]. Это значит, что каждый раз, когда нам нужно изменить что-то, изменяется не оригинальная структура, а создаётся новая

В [[Swift|swift]] существует оптимизация, позволяющая не выполнять копирование, если две переменные ссылаются на одни данные, а копировать только, когда происходит непосредственное изменение. Данный механизм называется **copy-on-write**.

Value types require a lot of copying, since assigning a value or passing it on as a function parameter creates a copy. While the compiler tries to be smart about this and avoid copies when it can prove it’s safe to do so, there’s another optimization the author of a value type can make, and that’s to implement the type using a technique called copy-on-write. This is especially important for types that can hold large amounts of data, like the standard library’s collection types (Array, Dictionary, Set, and String). They are all implemented using copy-on-write.

Copy-on-write means that the data in a **struct is initially shared among multiple variables**; the copying of the data is deferred until an instance mutates its data. Since arrays are implemented using copy-on-write, if we create an array and assign it to another variable, the array’s data hasn’t actually been copied yet.

```swift
var x = [1,2,3]
var y = x
```

Internally, the array values in `x` and `y` **contain a reference to the same memory buffer**.
This buffer is where the actual elements of the array are stored. However, the moment we mutate `x` (or `y` for that matter), the array detects that it’s sharing its buffer with one or more other variables and makes a copy of the buffer before applying the mutation

**Copy-on-write behavior is not something we get for free** for our own types; **we have to implement it ourselves,** just as the standard library implements it for its collection types. Implementing copy-on-write for a custom struct is only necessary in rare circumstances though, since the standard library already provides the most common types that deal with large amounts of data. Even if we define a struct that can contain a lot of data, **we’ll often use the built-in collection types to represent this data internally**, and as a result, we benefit from their copy-on-write optimizations.

## COW Tradeoffs
Copy-on-write **structs rely on storing a reference internally**, and the internal reference count has to be incremented for every copy of a struct that gets created. So we’re really giving up an advantage of value types — no need for reference counting — to mitigate against the potential cost of another property of value types — copy semantics.

**Incrementing or decrementing a reference count is a relatively slow operation** (compared to, say, copying a few bytes to another location on the stack) because **such an operation must be thread-safe and therefore incurs locking overhead**. Since all the variable-size types from the standard library — arrays, dictionaries, sets, and strings — rely on copy-on-write internally, all structs containing properties of these types also incur reference counting costs on each copy

A practical example for this comes from the [[SwiftNIO]] project: an [[SwiftNIO HTTP request]] used to be modeled as a struct in SwiftNIO, and it contained multiple properties like the HTTP method, headers, etc. When such a struct was copied, not only did all its fields have to be copied, but the reference counts for all internal arrays, dictionaries, and strings had to be incremented too.


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Advanced Swift]]