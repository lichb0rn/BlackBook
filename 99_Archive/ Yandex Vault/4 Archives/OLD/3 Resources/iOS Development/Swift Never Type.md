---
uuid: 20220828142305
created: 2022-08-28T14:23:05
alias:
- Never type
- тип Never
- uninhabited type
---

# [[Swift Never Type]]

A [[Swift|swift]] function with the return type `Never` signals to the compiler that it’ll never return. There are two common types of functions that do this: those that abort the program, such as `fatalError`; and those that run for the entire lifetime of the program, like `dispatchMain`. The compiler uses this information for its control flow diagnostics. For example, the else branch of a guard statement must either exit the current scope or call one of these never-returning functions.  

`Never` is what’s called an ***uninhabited type***. It’s a type that has no valid values and thus can’t be constructed. Never is useful in combination with `Result` in [[Swift Generics|generic]] contexts. For example, if a generic API expects a value of type `Result<A, E>` (where `A` and `E` are generic parameters), you can pass in a `Result<..., Never>` to signal that this concrete `Result` instance will never contain a failure because such a value is impossible to construct. What’s more, a function declared to return an uninhabited type can never return normally.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Advanced Swift]]