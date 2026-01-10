---
uuid: 20221012172339
created: 2022-10-12T17:23:39
alias:
- подмена зависимостей во время компиляции
- compile-time dependency substitution
tags:
---

# [[Compile-time substitution]]

To conditionally compile code in Swift, you add compilation condition identifiers to Xcode’s active compilation conditions build setting. Once you add custom identifiers to the active compilation condition’s build setting, you use the identifiers in `#if `and `#elseif` compilation directives.

You can use conditional compilation to change the dependency implementation that you want for a specific build configuration. For example, if you want to use a fake remote API implementation during tests:

- Create a Test build configuration.
- Change your target scheme’s Test scheme action’s build configuration to the Test build configuration created in the previous step.
- Add a TEST identifier to your target’s active compilation conditions build setting for the Test build configuration.
- Find the line of code wherein the consumer is creating a real remote API instance.
- Write an `#if `TEST compilation directive and, under the if statement, instantiate a fake remote API.
- Write an `#else` compilation directive and instantiate a real remote API under the else.
- Write an `#endif`  compilation directive on the next line to close the conditional compilation block.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]