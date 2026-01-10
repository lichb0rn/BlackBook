---
uuid: 20221110112548
created: 2022-11-10T11:25:48
alias:
- share()
---

# [[share() operator]]

The purpose of this operator is to let you obtain a [[Combine Publisher|publisher]] by reference rather than by value. Publishers are usually structs: When you pass a publisher to a function or store it in several properties, [[Swift]] copies it several times. When you subscribe to each of the copies, the publisher can only do one thing: Start the work it’s designed to do and deliver the values.

The `share()` operator returns an instance of the `Publishers.Share` class. Often, publishers are implemented as [[Swift Structures|structs]], but in `share()`s case, as mentioned before, the operator obtains a reference to the Share publisher instead of using value semantics, which allows it to share the underlying publisher.

This new publisher “shares” the upstream publisher. It will subscribe to the upstream publisher once, with the first incoming subscriber. It will then relay the values it receives from the upstream publisher to this subscriber and to all those that subscribe after it.

>[!note]
>New subscribers will **only receive values the upstream publisher emits after** they subscribe. There’s no buffering or replay involved. If a subscriber subscribes to a shared publisher after the upstream publisher has completed, that new subscriber only receives the completion event.

>[!note]
>A multicast publisher, like all `ConnectablePublishers`, also provides an `autoconnect()` method, which makes it work like `share()`: The first time you subscribe to it, it connects to the upstream publisher and starts the work immediately. This is useful in scenarios where the upstream publisher emits a single value and you can use a `CurrentValueSubject` to share it with subscribers.


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift]]
- 🏷️ Tags:: [[Combine]]