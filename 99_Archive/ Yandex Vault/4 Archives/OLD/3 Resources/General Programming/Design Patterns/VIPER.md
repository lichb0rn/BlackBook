---
uuid: 20221009153909
created: 2022-10-09T15:39:09
alias:
- VIPER
- "View-Interactor-Presenter-Entity-Router"
---

# [[VIPER]]

Each of the letters in _VIPER_ stand for a component of the architecture: _View_, _Interactor_, _Presenter_, _Entity_ and _Router_.

-   The _View_ is the user interface. This corresponds to a [[SwiftUI]] `View`.
-   The _Interactor_ is a class that mediates between the presenter and the data. It takes direction from the presenter.
-   The _Presenter_ is the “traffic cop” of the architecture, directing data between the view and interactor, taking user actions and calling to router to move the user between views.
-   An _Entity_ represents application data.
-   The _Router_ handles navigation between screens. That’s different than it is in SwiftUI, where the view shows any new views.

This separation is borne out of “Uncle” [[Robert Martin|Bob Martin's]] [[Clean Code A Handbook of Agile Software Craftsmanship|clean code]].
[![VIPER Diagram](https://koenig-media.raywenderlich.com/uploads/2020/02/viper-650x203.png)](https://koenig-media.raywenderlich.com/uploads/2020/02/viper.png)


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: https://www.raywenderlich.com/8440907-getting-started-with-the-viper-architecture-pattern#toc-anchor-012
- 🏷️ Tags:: [[Software Design Patterns]]