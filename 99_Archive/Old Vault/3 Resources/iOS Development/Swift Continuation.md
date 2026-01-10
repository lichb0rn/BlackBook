---
aliases: ["continuation"]
---
MOC:  [[Swift Concurrency Model]]

---

Есть два варианта continuation:

1. *CheckedContinuation*: A mechanism to resume a suspended execution or throw an error. It provides runtime checks for correct usage and logs any misuse.

2. *UnsafeContinuation*: An alternative to CheckedContinuation, but without the safety checks. Use this when performance is essential and you don’t need the extra safety.