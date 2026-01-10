---
uuid: 20221229123900
created: 2022-12-29T12:39:00
alias: memory binding
---

# [[Memory Binding]]

Memory binding means specifying an area in memory as a value of a specific type. For example, if you specify the four bytes between `0x0010` and `0x0013` as an `Int32`, this means you bound them to that type.

## Type Punning
Type punning is when a part of memory is bound to a type, then you bind it to a different and unrelated type.
```swift
let rawPointer = UnsafeMutableRawPointer.allocate(byteCount: 2, alignment: 2)
defer {
    rawPointer.deallocate()
  }
let float16Pointer = rawPointer.bindMemory(to: Float16.self, capacity: 1)
let uint8Pinter = rawPointer.bindMemory(to: UInt8.self, capacity: 2)

loat16Pointer.pointee = 0xABC0 // 43968

uint8Pointer.pointee // 0x5E = 94
uint8Pointer.advanced(by: 1).pointee // 0x79 = 121

uint8Pointer.pointee -= 1
float16Pointer.pointee // 43936
```

The binary representation of floats differs from integers. Thus, **any small changes in the binary representation will cause a more significant change in the value itself**.

## Relates types

To rebind from one type to another type safely, both types should be related and layout compatible, and should respect strict aliasing rules:
- Both types are identical or one is a [[typealias]] of the other.
- One type may be a tuple, a [[Swift Structures|struct]] or an enum that contains the other type.
- One type may be an **existential** (a [[Swift Protocol|protocol]]) that conforming types will contain the other type.
- Both types are [[Swift Class|classes]], and one is a subclass of the other.

## Layout compatibility

Two types are mutually layout compatible means **they have the same size and alignment or contain the same number of layout compatible types**.

Types can be layout compatible but not *mutually*. They’re compatible if one aggregate type is layout compatible with a larger type containing the same common types. For example, the tuple `(Int,Int)` is memory compatible with `(Int,Int,Float)` because they both have the same common types, but they aren’t mutually compatible.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]
-  🏷️ Tags:: [[Swift]]