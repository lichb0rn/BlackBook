---
uuid: 20220928063418
created: 2022-09-28T06:34:18
alias:
---

# [[Gradient text animation]]

Предположим мы хотим создать анимированный градиентый текст (slide to reveal).
Создаём градиент и текстовые атрибуты:
```swift
let gradientLayer: CAGradientLayer = {
	let gradientLayer = CAGradientLayer()
	gradientLayer.startPoint = CGPoint(x: 0.0, y: 0.5)
	gradientLayer.endPoint = CGPoint(x: 1.0, y: 0.5)
	let colors = [
		UIColor.black.cgColor,
		UIColor.white.cgColor,
		UIColor.black.cgColor
	]
	gradientLayer.colors = colors
	let locations: [NSNumber] = [0.25, 0.5, 0.75]
	gradientLayer.locations = locations
	
	return gradientLayer
}()
    
let textAttributes: [NSAttributedString.Key: Any] = {
	let style = NSMutableParagraphStyle()
	style.alignment = .center
	return [
		.font: UIFont.systemFont(ofSize: 28, weight: .thin),
		.paragraphStyle: style
	]
}()
```

Задаём frame и анимацию:
```swift
override func layoutSubviews() {
	layer.borderColor = UIColor.green.cgColor
	gradientLayer.frame = CGRect(x: -bounds.size.width,
								 y: bounds.origin.y,
								 width: 3 * bounds.size.width,
								 height: bounds.size.height)
}

override func didMoveToWindow() {
	super.didMoveToWindow()
	layer.addSublayer(gradientLayer)
	
	let gradientAnimation = CABasicAnimation(keyPath: "locations")
	gradientAnimation.fromValue = [0, 0, 0.25]
	gradientAnimation.toValue = [0.75, 1, 1]
	gradientAnimation.duration = 3
	gradientAnimation.repeatCount = Float.infinity
	
	gradientLayer.add(gradientAnimation, forKey: nil)
}
```

Наконец рисуем текст как картинки и делаем его маской для градиента:
```swift
@IBInspectable var text: String = "" {
	didSet {
		setNeedsDisplay()
		let image = UIGraphicsImageRenderer(size: bounds.size)
			.image { _ in
				text.draw(in: bounds, withAttributes: textAttributes)
			}
		let maskLayer = CALayer()
		maskLayer.backgroundColor = UIColor.clear.cgColor
		maskLayer.frame = bounds.offsetBy(dx: bounds.size.width, dy: 0)
		maskLayer.contents = image.cgImage
		gradientLayer.mask = maskLayer
	}
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[iOS Animations by Tutorials]]
- 🏷️ Tags:: [[UIKit]], [[Design]], [[User Experience]]