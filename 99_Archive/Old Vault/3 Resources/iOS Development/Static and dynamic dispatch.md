---
uuid: 20221105081419
created: 2022-11-05T08:14:19
alias:
- static dispatch
- dynamic dispatch
- witness table
- v-table
tags:
---

# [[Static and dynamic dispatch]]

At runtime, when [[Swift|Swift]] finds a function name, it jumps to the address of that function and starts executing the code. But jumping to a function’s address is not always straightforward. 

There are two main mechanisms for storing and calling functions: **static** and **dynamic** dispatch. 

## Static dispatch

Static dispatch is fairly straightforward: It happens when you know for sure that a function will never change. 

Static dispatch is used, among other reasons, for global functions and methods declared in structs as well as methods on `final` [[Swift Class|classes]]. 

In those cases, there is no function overriding to worry about, so the compiler can, in a sense, hard-code the function’s address and hop to that whenever the function is referenced.

>[!note] Aside from method dispatch, there is also a technique called inlining that Swift uses extensively. Inlining replaces a function call with the full body of that function at compile time. This is the fastest way to call a function, but it’s only available with static dispatch and under specific conditions.

## Dynamic dispatch

When you add inheritance and [[Swift Protocol|protocols]], things get a bit more complicated. 
A method called on a non-final class instance can be declared in multiple possible places. 

It can be declared inside the class, any of its parent classes, an extension or even a protocol extension. This means the compiler can’t know ahead of time what the exact address of a function will be. 

Instead, it uses something called the **witness table** (sometimes also called the v-table or the virtual table).

As the compiler goes through your code, it will create a table for each class. 
This table will have two columns: one for an offset in the table and one for the function at that offset. 

Each function in the class is stored in the table, which is stored in your working memory. 
A subclass will get a copy of its parent’s table and then replace the rows of the method it wants to override. 

Now that a witness table is built, Swift can use the table at runtime. 
When it encounters a method call, Swift knows which offset in the table corresponds to that method.  

This allows dynamic changing of the implementation of a method with the same name, allowing features like inheritance, polymorphism and even protocols. But these features come at a cost. Calling functions from table rows adds a constant overhead for each function call. 

It also prevents inlining and other compiler optimizations, making dynamic dispatch slower than static dispatch.

Every type that implements a protocol gets its own protocol witness table. The table has two columns again, one with the function and the other with the offset of that function. Each member of the protocol (the methods and variables declared as the protocol requirements) has its own row in the table. This table is then stored together with each instance that implements a protocol. Swift can then, at runtime, look up the correct function in the protocol witness table and call it. If you’re using a class instance, Swift can look the function up in both the class and the protocol witness table, dynamically finding the correct implementation.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]