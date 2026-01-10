---
uuid: 20221016201410
created: 2022-10-16T20:14:10
alias:
- class instantiation in python
- инициализация класс в python
- "__init__"
tags:
---

# [[Инициализация класса в Python]]

В [[Python]] инициализация класса проходит в несколько этапов:
- Our code asks [[Python]] to create an object from the `LightSwitch`  class.
- [[Python]] allocates space in memory for a  `LightSwitch`  object, then calls the `___init__()` method of the  `LightSwitch`  class, passing in the newly created object.
- The ` ___init__()`  method of the  `LightSwitch` class runs. The new object is assigned to the parameter `self`. The code of `___init__()` initializes any instance variables in the object (in this case, the instance variable `self.switchIsOn`).
- [[Python]] returns the new object to the original caller
- The result of the original call is assigned into the variable `oLightSwitch`, so it now represents the object.
![[Pasted image 20221016201602.png]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Object-Oriented Python]]