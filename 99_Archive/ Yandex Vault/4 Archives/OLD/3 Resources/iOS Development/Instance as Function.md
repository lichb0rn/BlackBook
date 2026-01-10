---
uuid: 20220927155142
created: 2022-09-27T15:51:42
alias:
- instance as function
---

# [[Instance as Function]]

Sometimes a type’s primary job is to contain or represent a function. In those situations, it makes for cleaner code if we can treat an instance of that type as a function. The ability to do that was introduced in [[Swift|Swift]] 5.2.

Imagine I have a struct `Adder`, whose job is to store a base value and add it to any addend we care to supply:

```swift
let add3 = Adder(3)
let sum = add3(4)
print(sum) // 7
```

`add3` is not a function! It is an instance of a [[Swift Structures|struct]]. We are treating an instance as a function.

The implementation, behind the scenes, is simple. If a type declares an instance method named `callAsFunction`, you can “call” an instance of that type as if it were a function: the “call” is routed to the `callAsFunction` method. Here’s `Adder`:

```swift
struct Adder {
	let base: Int
	
	init(_ base:Int) {
		self.base = base
	}

	func callAsFunction(_ addend:Int) -> Int {
		return self.base + addend
	}
}
```


You can give your type multiple `callAsFunction` overloads, distinguished in the usual way by parameter types, parameter labels, or both. In this way, a single instance can behave as if it were itself an overloaded function.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[iOS 15 Programming Fundamentals with Swift]]