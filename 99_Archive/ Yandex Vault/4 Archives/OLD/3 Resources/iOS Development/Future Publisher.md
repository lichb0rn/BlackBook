---
uuid: 20221030125642
created: 2022-10-30T12:56:42
alias:
- future publisher
---

# [[Future Publisher]]

You create a Future by handing it a closure which receives a Promise argument. You further fulfill the promise whenever you have a result available, either successful or failed.

- `Future` is a [[Swift Class|class]], not a struct.
- Upon creation, it immediately invokes your closure to start computing the result and fulfill the promise as soon as possible.
- It stores the result of the fulfilled Promise and delivers it to current and future subscribers.

In practice, it means that `Future` is a convenient way to immediately start performing some work (without waiting for subscriptions) while performing work only once and delivering the result to any amount of subscribers. But it performs work and returns a single result, not a stream of results, so the use cases are narrower than full-blown publishers.

It‘s a **good candidate to use for when you need to share the single result** a network request produces.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift]]
- Additional link:: https://www.swiftbysundell.com/articles/under-the-hood-of-futures-and-promises-in-swift/
- 🏷️ Tags:: [[Combine]]