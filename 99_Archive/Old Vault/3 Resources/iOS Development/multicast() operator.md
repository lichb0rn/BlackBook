---
uuid: 20221110113317
created: 2022-11-10T11:33:17
alias:
tags:
---

# [[multicast() operator]]

This operator builds on [[share() operator]] and uses a [[Combine Subject]] of your choice to publish values to subscribers. The unique characteristic of `multicast(_:)` is that the [[Combine Publisher|publisher]] it returns is a `ConnectablePublisher`. What this means is it won’t subscribe to the upstream publisher until you call its `connect()` method. This leaves you ample time to set up all the subscribers you need before letting it connect to the upstream publisher and start the work.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift]]