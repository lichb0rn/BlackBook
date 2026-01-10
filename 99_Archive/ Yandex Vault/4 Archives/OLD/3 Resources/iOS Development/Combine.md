---
uuid: 20221022200931
created: 2022-10-22T20:09:31
alias: Combine framework
---

# [[Combine]]

The Combine framework provides a declarative [[Swift|Swift]] API for processing values over time. These values can represent many kinds of asynchronous events. Combine declares _publishers_ to expose values that can change over time, and _subscribers_ to receive those values from the publishers.

-   The [[Combine Publisher|Publisher]](https://developer.apple.com/documentation/combine/publisher) [[Swift Protocol|protocol]] declares a type that can deliver a sequence of values over time. Publishers have [[Combine Operators|operators]] to act on the values received from `upstream` publishers and republish them.
-   At the end of a chain of publishers, a [[Combine Subscriber|Subscriber]](https://developer.apple.com/documentation/combine/subscriber) acts on elements as it receives them. Publishers only emit values when explicitly requested to do so by subscribers. This puts your subscriber code in control of how fast it receives events from the publishers it’s connected to.

## Subscription cycle
![[Pasted image 20221128150253.png|450]]
1. Publisher receives the subscriber and creates a Subscription
2. Subscriber receives the subscription and requests values from the publisher (dotted lines).
3. Publisher starts work (via the Subscription).
4. Publisher emits values (via the Subscription).
5. Operators transform values.
6. Subscriber receives the final values.

Steps one, two and three usually happen on the thread that is current when your code subscribes to the publisher.
More: [[Subscription Lifecycle]]

## Handling backpressure
[[Combine]]'s publisher-subscriber mechanism is a *pull* design. **Subscribers ask publishers to emit values and specify how many they want to receive.** The demand updates every time the subscriber receives a new value. This allows subscribers to deal with backpressure by "closing the tap" when they don’t want to receive more data, and "opening it" later when they are ready for more.
>[!note]
>You can only adjust demand in an additive way. You can increase demand each time the subscriber receives a new value, by returning a new .max(N) or .unlimited. Or you can return .none, which indicates that the demand should not increase. However, the subscriber is then "on the hook" to receive values at least up to the new max demand. For example, if the previous max demand was to receive three values and the subscriber has only received one, returning .none in the subscriber’s receive(_:) will not "close the tap." The subscriber will still receive at most two values when the publisher is ready to emit them.



### Links

[[Future Publisher]]
[[share() operator]]
[[multicast() operator]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source::  https://developer.apple.com/documentation/combine
- 📖 Book:: [[Combine Asynchronous Programming with Swift]]
- 🏷️ Tags:: [[iOS Development]], [[Asynchronous Programming]]