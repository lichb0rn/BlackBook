---
uuid: 20220720191737
created: 2022-07-20T19:17:37
alias:
- es
- esm
---

# [[ECMAScript modules]]

The most important differentiator between ESM and [[CommonJS]] is that **ES modules
are static**, which means that **imports are described at the top level of every module**
and **outside any control flow statement**. Also, the name of the imported modules
cannot be dynamically generated at runtime using expressions, only constant strings
are allowed.

Static imports **allow the static analysis of the dependency tree**, which allows optimizations such as dead code elimination (**tree shaking**) and more.

## Using ESM in [[Node.js]]
[[Node.js ]]will consider every `.js` file to be written using the [[CommonJS]] syntax by default; therefore, if we use the ESM syntax inside a `.js` file, the interpreter will simply throw an error.

There are several ways to tell the Node.js interpreter to consider a given module as
an ES module rather than a CommonJS module:
- Give the module file the extension` .mjs`
- Add to the nearest parent `package.json` a field called `"type"` with a value of `"module"`

In an ES module, **everything is private by default** and **only exported entities are publicly accessible** from other modules.

## Loading phases
The goal of the interpreter is to build a graph of all the necessary modules (a **dependency graph**). In generic terms, a dependency graph can be defined as a [[Граф (теория)#Ориентированные и неориентированные графы|directed graph]] (nodejsdp.link/directed-graph) representing the dependencies of a group of objects. 

When the node interpreter is launched, it gets passed some code to execute, generally in the form of a [[JavaScript]] file. This file is the starting point for the dependency resolution, and it is called the entry point. From the entry point, the interpreter will find and follow all the import statements recursively in a [[Обход графа|depth-first]] fashion, until all the necessary code is explored and then evaluated.

### Three separate phases
- **Phase 1 - Construction (or parsing)**: Find all the imports and recursively load the content of every module from the respective file.
- **Phase 2 - Instantiation**: For every exported entity, **keep a named reference** in memory, but **don't assign any value** just yet. Also, references are created for all the import and export statements tracking the dependency relationship between them (**linking**). **No [[JavaScript]] code has been executed at this stage**.
- **Phase 3 - Evaluation**: [[Node.js]] finally **executes the code** so that all the previously instantiated entities can get an actual value. **Now** **running the code from the entry point is possible** because all the blanks have been filled.

At first glance, this approach doesn't seem very different from what [[CommonJS]] does, but **there's a fundamental difference**. Due to its dynamic nature, [[CommonJS]] will execute all the files while the dependency graph is explored. 

In ESM, these **three phases are totally separate from each other**, no code can be executed until the dependency graph has been fully built, and therefore **module imports and exports have to be static**.

When an entity is imported in the scope, the **binding to its original value cannot be changed** (***read-only binding***) unless the bound value changes within the scope of the original module itself (live binding), which is outside the direct control of the consumer code. This approach is fundamentally different from [[CommonJS]]. In fact, in [[CommonJS]], the entire exports object is copied (shallow copy) when required from a module.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]