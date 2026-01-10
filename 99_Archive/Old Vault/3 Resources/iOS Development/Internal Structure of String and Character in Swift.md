---
uuid: 20220913203322
created: 2022-09-13T20:33:22
alias:
- internal string structure in swift
- swift string optimizations
---

# [[Internal Structure of String and Character in Swift]]

Like the other collection types in the standard library, strings are [[Copy-on-Write|copy-on-write]] collections with [[Swift Structures|value semantics]]. A [[Swift Strings|String]] instance stores a reference to a buffer, which holds the actual character data. When you make a copy of a string (through assignment or by passing it to a function) or create substrings, all these instances share the same buffer. 

As of [[Swift|Swift]] 5, String uses [[UTF-8]] as its in-memory representation for native Swift strings. You may be able to use this knowledge to your advantage if you require the best possible performance — traversing the [[UTF-8]] view may be a bit faster than the [[UTF-16]] or [[Unicode]] scalar views. Also, UTF-8 is the natural format for most string processing, because the majority of source data from files or the web uses the UTF-8 encoding.

For small strings of up to 15 UTF-8 code units (or 10 code units on 32-bit platforms) there’s a special optimization that avoids allocating a backing buffer altogether. Since strings are 16 bytes wide, the code units of small strings can be stored inline.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Advanced Swift]]