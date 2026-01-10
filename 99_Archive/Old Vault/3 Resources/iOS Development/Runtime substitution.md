---
uuid: 20221012172845
created: 2022-10-12T17:28:45
alias:
- подмена зависимостей во время выполнения
- runtime dependency substitution
tags:
---

# [[Runtime substitution]]

To substitute an implementation at runtime, you write an if statement around the dependency instantiation. You need to decide where to get a value that you can use to compare in the if statement. For example, you can use a remote-feature flag service, or you can key off local values, such as the app’s version number.

Another neat trick is to use launch arguments to substitute dependencies at runtime. This is useful when you’re developing an app in [[Xcode]]. This is neat because you don’t need to recompile the app to change dependency implementations. Simply grab the launch arguments from [[UserDefaults]] and wrap your dependency instantiations with if statements that check launch argument values. You can use this trick during development or even during a continuous integration test.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]