---
uuid: 20221022201542
created: 2022-10-22T20:15:42
alias:
tags:
---

# [[Combine Subscriber]]

Subscribers generally do "something" with the emitted output or completion events.
[[Combine]] provides two built-in subscribers, which make working with data streams straightforward:
- The `sink` subscriber allows you to provide closures with your code that will receive output values and completions. From there, you can do anything your heart desires with the received events.
- The `assign` subscriber allows you to, without the need of custom code, bind the resulting output to some property on your data model or on a UI control to display the data directly on-screen via a [[Swift KeyPath|key path]].

## Subscription

When you add a subscriber at the end of a subscription, it "activates" the [[Combine Publisher|publisher]] all the way at the beginning of the chain. This is a curious but important detail to remember — **publishers do not emit any values if there are no subscribers to potentially receive** the output.

Both system-provided subscribers conform to [[Cancellable]], which means that your subscription code (e.g. the whole publisher, operators and subscriber call chain) returns a Cancellable object. Whenever you release that object from memory, **it cancels the whole subscription and releases its resources from memory.**

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift]]