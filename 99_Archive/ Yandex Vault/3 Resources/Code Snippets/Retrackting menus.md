---
uuid: 20220919165910
created: 2022-09-19T16:59:10
alias:
---

# [[Retrackting menus]]

```swift
@IBAction func actionToggleMenu(_ sender: AnyObject) {
    guard
        let titleLabel = titleLabel,
        let titleSuperview = titleLabel.superview else { return }
        
    isMenuOpen.toggle()
        
    titleLabel.superview?.constraints.forEach { constraint in
       if constraint.firstItem === titleLabel 
       && constraint.firstAttribute == .centerX {
	       constraint.constant = isMenuOpen ? -100 : 0.0
           return
        }
            
        if constraint.identifier == "TitleCenterY" {
            constraint.isActive = false
         
	        let newConstraint = NSLayoutConstraint(
                item: titleLabel,
                attribute: .centerY,
                relatedBy: .equal,
                toItem: titleSuperview,
                attribute: .centerY,
                multiplier: isMenuOpen ? 0.67 : 1.0,
                constant: 0
            )
            newConstraint.identifier = "TitleCenterY"
            newConstraint.isActive = true
              
            return
        }
    }
        
        menuHeightConstraint.constant = isMenuOpen ? 184.0 : 44.0
        titleLabel.text = isMenuOpen ? "Select Item" : "Packing List"
        
        UIView.animate(withDuration: 1.0, delay: 0,
                       usingSpringWithDamping: 0.4, initialSpringVelocity: 10,
                       options: .curveEaseIn) {
            self.view.layoutIfNeeded()
            
            let angle: CGFloat = self.isMenuOpen ? .pi / 4 : 0
            self.buttonMenu.transform = CGAffineTransform(
	            rotationAngle: angle)
        }
    }
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[iOS Animations by Tutorials]], p 100, Chapter 9: Animating Constraints
- 🏷️ Tags:: [[UIKit]]