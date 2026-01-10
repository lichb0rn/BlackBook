---
uuid: 20221219185955
created: 2022-12-19T18:59:55
alias: 
- pointer
- UnsafeRawPointer
- UnsafePointer
---

# [[Pointer Types]]

Swift provides different pointer types. Each provides its own control safety levels or unsafety levels.
- `UnsafeRawPointer`
	- the basic raw pointer that doesn’t know any information of the type it is pointing at. It’s a basic pointer on a specific byte.
- `UnsafePointer<Type>`
	- a pointer that knows the type of the object it points at. It’s also called a typed pointer.

**Raw pointers can’t work on reference or non-trivial types. For those, you must use a typed pointer.**

If you’re working with arrays, there’s a set of pointer types that can make things a little easier for you:
- `UnsafeRawBufferPointer
- `UnsafeBufferPointer<Type>`

All those pointers are read-only access. To allow read-and-write access, you need mutable pointers. Any of the above pointer types can be mutable, as seen below:
- `UnsafeMutableRawPointer`
- `UnsafeMutablePointer<Type>`
- `UnsafeMutableRawBufferPointer`
- `UnsafeMutableBufferPointer<Type>`

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]
-  🏷️ Tags:: [[Swift]]