---
aliases: ["sprout method"]
---
MOC:  [[Software Development MOC]]

---

	A technique called sprouting a method, which is when you add a new method in an existing class that enhances or duplicates existing functionality so you can add a new feature. This technique allows you to sidestep going down a hole refactoring a class or potentially breaking things not yet under test. It allows you to define a new interface, cleanly separated from the legacy part of the code. 