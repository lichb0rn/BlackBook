---
uuid: 20230312133141
created: 2023-03-12T13:31:41
alias:
---

# [[Effect Sketches]]

The key is t**o have a separate bubble for each variable that can be affected and each method whose return value can change**. Sometimes the variables are on the same object, and sometimes they are on different objects. It doesn’t matter: We just make a bubble for the things that will change and draw an arrow to everything whose value can change at runtime because of them.

Here is a heuristic that I use when looking for effects:
1. Identify a method that will change.
2. If the method has a return value, look at its callers.
3. See if the method modifies any values. If it does, look at the methods that use those values, and the methods that use those methods.
4. Make sure you look for superclasses and subclasses that might be users of these instance variables and methods also.
5. Look at parameters to the methods. See if they or any objects that their methods return are used by the code that you want to change.
6. Look for global variables and static data that is modified in any of the methods you’ve identified.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source::  [[Working Effectively with Legacy Code]]
-  🏷️ Tags:: [[Refactoring]]