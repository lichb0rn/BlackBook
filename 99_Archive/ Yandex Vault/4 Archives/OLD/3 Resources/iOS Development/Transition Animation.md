---
uuid: 20221003112246
created: 2022-10-03T11:22:46
alias:
- transition
- UIViewControllerContextTransitioning
- UIViewControllerAnimatedTransitioning
- анимация перехода
---

# [[Transition Animation]]

## Transition Context

When the transition between the two view controllers begins, the existing view is added to a transition container view and the new view controller’s view is created but not yet visible.

Therefore your task is to add the new view to the transition container within `animateTransition()`, “animate in” it's appearance, and “animate out” the old view if required.

By default, the **old view is removed from the transition container when the transition animation is done**.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[iOS Animations by Tutorials]]
- 🏷️ Tags::