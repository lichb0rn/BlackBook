---
uuid: 20220209161209
created: 2022-02-09T16:12:09
alias:
- retain cycle
- memory management
- ARC
tags:
---

# [[Swift Memory Management]]

By default, a reference is a strong reference: assigning to it retains the assigned value. In [[Swift|Swift]], you can declare a reference type variable as weak or as unowned to change the way its memory is managed:
-   `weak`
**When a reference is weak, [[ARC]] does not retain the object assigned to it.**
A reference marked as weak must be a var reference to an `Optional`. ARC keeps track of all weak references and all objects assigned to them. When such an object’s retain count drops to zero and the object is about to be destroyed, just before the object’s `deinit` is called, ARC sneaks in and assigns nil to all weak references to the object. Provided you handle the [[Swift Optionals|Optional]] coherently (by coping with the fact that it might suddenly be `nil`), nothing bad can happen.

-   `unowned`
An unowned reference is a different kettle of fish. When you mark a reference as `unowned`, you’re telling ARC to take its hands off completely: **it does no memory management at all** when something is assigned to this reference. This really is dangerous — if the object referred to goes out of existence, you really can be left with a dangling pointer and you really can crash. That is why you must never use unowned unless you know that the object referred to will not go out of existence: unowned is safe, provided the object referred to will outlive the object that refers to it. So an unowned reference should point to an independent object, retained in some other way, without which the referrer cannot exist at all.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[iOS 15 Programming Fundamentals with Swift]]