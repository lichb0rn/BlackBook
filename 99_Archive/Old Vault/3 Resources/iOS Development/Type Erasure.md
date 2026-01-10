---
uuid: 20221024100405
created: 2022-10-24T10:04:05
alias:
tags:
---

# [[Type Erasure]]

## Combine
Type Erasure для [[Combine]]:
```swift
example(of: "Type erasure") {
    let subject = PassthroughSubject<Int, Never>()
    let publisher = subject.eraseToAnyPublisher()

    publisher
        .sink(receiveValue: { print($0) })
        .store(**in**: &subscriptions)
    subject.send(0)
}
```

[[AnyPublisher]] is a type-erased [[Swift Structures|struct]] that conforms the [[Combine Publisher|Publisher]] protocol. Type erasure allows you to hide details about the publisher that you may not want to expose to subscribers — or downstream publishers, which you’ll learn about in the next section.

One example of when you would want to use type erasure for a publisher is when you want to use a pair of public and private properties, to allow the owner of those properties to send values on the private publisher, and let outside callers only access the public publisher for subscribing but not be able to send values.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift]]