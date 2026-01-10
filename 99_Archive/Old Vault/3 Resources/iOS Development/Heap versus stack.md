---
uuid: 20221029201510
created: 2022-10-29T20:15:10
alias:
tags:
---

# [[Heap versus stack]]

A general rule of thumb is that classes use heap memory but structures and enumerations use stack memory. Because stack allocations are orders of magnitude faster than heap allocations, this is where value types get their fast reputation.

Each thread of execution has its own stack, and stacks only change by modifying the top-most element. As a result, allocating and deallocating onto a stack doesn’t require expensive concurrency locks or fancy allocation strategies. Allocation and deallocation can be performed with a single add or subtract instruction in a single clock tick.

The heap, by contrast, is shared by multiple threads and needs to be protected by concurrency locks. The operating system must protect against heap fragmentation, which can happen if you allocate and deallocate different size memory blocks. As a result, even though heap allocation has been highly optimized, it’s ultimately non-deterministic and could require thousands or even millions of instructions to perform.  

>[!note]
>Heap for classes vs. stack for structures and enumerations is just a general rule of thumb. As you saw in the previous chapter, the **Swift compiler starts by allocating everything on the heap and then reasons about the object’s lifetime to determine whether it can be allocated on the stack**. For example, an escaping closure that closes over a local structure will need to put that object on the heap to extend the structure’s lifetime beyond its scope. On the other hand, a class that is created, that performs some action and then goes out of scope might be optimized away entirely and just include the instructions necessary to complete the operation.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]