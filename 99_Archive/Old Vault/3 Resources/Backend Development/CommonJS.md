---
uuid: 20220717164107
created: 2022-07-17T16:41:07
alias: cjs
---

# [[CommonJS]]

CommonJS is the first module system originally built into [[Node.js]]. Node.js'
CommonJS implementation respects the CommonJS specification, with the addition
of some custom extensions.

Two main concepts:
- `require` is a function that allows you to import a module from the local filesystem
- `exports` and `module.exports` are special variables that can be used to export
public functionality from the current module.


## `module.exports` vs `exports`
The `exports` variable is just a reference to the initial value of `module.exports`.


## How cjs resolves dependencies
[[CommonJS Dependency Management]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]