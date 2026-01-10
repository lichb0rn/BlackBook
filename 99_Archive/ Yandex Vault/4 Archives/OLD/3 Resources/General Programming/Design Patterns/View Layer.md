---
uuid: 20221023162016
created: 2022-10-23T16:20:16
alias:
- view layer
- слой представления
tags:
---

# [[View Layer]]

A view is a user interface for a screen. In [[Model-View-ViewModel|MVVM]], the view layer reacts to state changes through bindings to view model properties. It also notifies the view model of user interaction, like button taps or text input updates.

The purpose of the view is to render the screen. It knows how to layout and style the user interface elements, but doesn’t know anything about business logic.

In MVVM, you use one-way data binding to bind the UI elements from the view to the view model. This means the view model is the single source of truth. The view doesn’t update until the view model changes its state.

The view layer contains a hierarchy of views. Each parent view knows about its children and has access to their properties.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]