---
uuid: 20221009073211
created: 2022-10-09T07:32:11
alias:
- VIP
- "View-Interactor-Presenter"
---

# [[VIP Architecture pattern]]

The VIP architecture for writing clean [[Swift|Swift]] code was introduced by [[Raymond Law]]. He created a [clean-swift](https://clean-swift.com/) website where you can read about how to use VIP [[Software Design Patterns|design patterns]] in [[UIKit]].

What does VIP stand for then? _View_ – Interactor – _Presenter_.

The VIP pattern is a _unidirectional_ architectural pattern. You might have already heard of some others, such as [[Redux]], [[Flux]] or [[Model-View-Intent]] (MVI). These patterns focus on reactive UIs and state management. 

Unidirectional patterns share one property: **Their components are all interconnected and aren’t designed to mix. Each has its own clear responsibility.**
![[Pasted image 20221009073807.png]]

Each letter in VIP stands for one component: _View_, _Interactor_ and _Presenter_.

-   The **_View_** is your app’s UI. This corresponds to a [[SwiftUI]] `View`. It sends requests to the interactor every time the user interacts with the UI.
-   The **_Interactor_** handles your app’s business logic, such as fetching data from the network or saving data in a database. When the view requests something, the interactor does the processing and sends the result as a response to the presenter.
-   The **_Presenter_** handles the presentation logic. It formats the received data into view models suitable for display and then passes it to the view.


## Models
_Data Models_ in VIP are decoupled data abstractions. They pass the data between components and consist of only primitive types such as `Int`, `Double` or `String`. 

You could create `Struct`, `Class` or `Enum`, but if the business logic changes, the underlying data models change. Using primitive types makes it easier to change the components without needing to update the entire codebase.
![[Pasted image 20221009074138.png]]

The typical user interaction goes like this: The cycle starts in the view when the user taps a button in the app’s UI. 

The view creates a _Request_ object and sends it to the interactor. The interactor takes the request object, performs work and sends the result as a _Response_ to the presenter. The presenter then takes the response, formats the data into primitive types and sends the result as a [[Model-View-ViewModel|_ViewModel_]] back to the view.

Then, finally, the view displays results to the user. 

These three payloads make the data model:

-   _Request_
-   _Response_
-   _ViewModel_

## Workers
You can have multiple workers for the interactor, with each handling a specific logic. If your app fetched the data from an API, you’d create a _NetworkWorker_ and have all the networking logic inside. If your app saved the data using [[Core Data|CoreData]], you’d add a _CoreDataWorker_ and so on.
![[Pasted image 20221009083841.png]]

## Configurator
The configurator’s job is to instantiate and connect the components of the VIP cycle. This is where you create the unidirectional cycle between the VIP components. There’s only one configurator for every scene and you need to call it only once, so you’ll create it in a separate file.

The view loads when the app starts, but you need to create presenter and interactor instances manually.

## Navigation using Router
The router component has two protocols: _RoutingLogic_ and _DataStore_. 

_RoutingLogic_ contains navigation methods. If your view navigates to multiple views, the router handles all.

_DataStore_ contains the data you need to pass to the destination view. You create it inside the interactor. That way, the router can get the data it needs to pass to another view and doesn’t know about the interactor.

![[Pasted image 20221009112716.png]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source::  [Raywenderlich](https://www.raywenderlich.com/29416318-getting-started-with-the-vip-clean-architecture-pattern)
- 🏷️ Tags:: [[Software Design Patterns]]