---
uuid: 20221023161351
created: 2022-10-23T16:13:51
alias:
- MVVM
- "model-view-viewmodel"
tags:
---

# [[Model-View-ViewModel]]

MVVM is a “reactive” architecture. The view reacts to changes on the view model, and the view model updates its state based on data from the model.

MVVM involves three layers:
- The [[Model layer|model layer]] contains data access objects and validation logic. It knows how to read and write data, and it notifies the view model when data changes.
- The [[ViewModel Layer|view model layer]] contains the state of the view and has methods to handle user interaction. It calls methods on the model layer to read and write data, and it notifies the view when the model’s data changes.
- The [[View Layer|view layer]] styles and displays on-screen elements. It doesn’t contain business or validation logic. Instead, it binds its visual elements to properties on the view model. It also receives user inputs and interaction, and it calls methods on the view model in response.

As a result, the view layer and model layer are completely decoupled. The view layer and model layer only communicate with the view model layer.
![[Notifies on.jpeg]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]