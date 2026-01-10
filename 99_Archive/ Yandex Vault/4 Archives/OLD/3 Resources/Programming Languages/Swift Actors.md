---
uuid: 20220821142429
created: 2022-08-21T14:24:29
alias: fetch data in a SwiftUI app
---

# [[Swift Actors]]

**Full Question: Hi there! What’s the recommended way to repeatedly fetch data in a SwiftUI app, (so that we don’t push updates from a different thread)?** 

Answer: In general, I would suggest to factor out the logic that fetches the data into its own type. You always want to execute this kind of side effect not on the main thread and the hop back onto the main thread to set the data on the model.

Swift’s actors are a great tool to encapsulate this kind of logic. So for example you could the model that is offered to the view be an ObservableObject that is bound to the main actor, and have a separate actor (hence running on a separate thread) that takes care of the fetching and report back new data to your observable object.  [Source](https://swiftui-lab.com/digital-lounges-2022/) 

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note