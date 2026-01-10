---
uuid: 20221010152400
created: 2022-10-10T15:24:00
alias:
- расширяемая ячейка таблица
- cell with toggle
---

# [[Expandable Table View Cell]]

Если мы хотим реализовать ячейку [[UITableView]] с кнопкой, которая будет динамически менять высоту, то можно сделать так:

Сначала подкидываем таблицу в ячейку в `tableView(_:UITableView, cellForRowAt:)`:
```swift
let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", 
										 for: indexPath) 
    if let widgetCell = cell as? WidgetCell {
        widgetCell.tableView = tableView
        widgetCell.owner = self
    }
```

В самой ячейке ссылка на таблицу хранится как `weak var tableView: UITableView?`.

Далее в ячейке определяем необходимые методы:
```swift
class WidgetCell: UITableViewCell {
    private var showsMore = false
    @IBOutlet weak var widgetHeight: NSLayoutConstraint!
    
    weak var tableView: UITableView?
    var toggleHeightAnimator: UIViewPropertyAnimator?
    
    @IBOutlet weak var widgetView: WidgetView!
    
    var owner: WidgetsOwnerProtocol? {
        didSet {
            if let owner = owner {
                widgetView.owner = owner
            }
        }
    }
    
    @IBAction func toggleShowMore(_ sender: UIButton) {
        self.showsMore.toggle()
        
        let animations = {
            self.widgetHeight.constant = self.showsMore ? 230 : 130
            if let tableView = self.tableView {
                tableView.beginUpdates()
                tableView.endUpdates()
                tableView.layoutIfNeeded()
            }
        }
        
        let spring = UISpringTimingParameters(
            mass: 30,
            stiffness: 1000,
            damping: 300,
            initialVelocity: CGVector(dx: 5, dy: 0)
        )
        toggleHeightAnimator = UIViewPropertyAnimator(duration: 0, timingParameters: spring)
        toggleHeightAnimator?.addAnimations(animations)
        toggleHeightAnimator?.startAnimation()
        
        widgetView.expanded = showsMore
        widgetView.reload()
    }
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source::  [[iOS Animations by Tutorials]], Chapter 23
- 🏷️ Tags:: [[UICollectionView]], [[UITableView]]