---
aliases: ["swiftui layout"]
---
MOC:  [[SwiftUI]]

---

Layout starts from the top of the view hierarchy. The parent view tells its children, “I propose this size”. Each child then takes as much room as it needs within the parent’s available space and tells the parent “I only need this size”. This continues all the way down the view hierarchy. The parent then resizes itself to the size of its child views.