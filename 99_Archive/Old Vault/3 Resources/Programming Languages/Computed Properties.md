---
aliases: ['# Computed properties']
tags: ['']
---

MOC: [[Swift]]

# Computed properties

В дополнение к [[Stored Properties]], [[Swift Class|классы]], [[Swift Structures|структуры]] и [[Swift Enumeration|перечисления]] могут определяет вычисляемые свойства. Такие свойства не хранят значение, вместо этого они предоставляют [[Swift Class|getter]] и опционально [[Swift Class|setter]] для получения и записи значений.

```swift
struct Point {
	var x = 0.0, y = 0.0
}
struct Size {
	var width = 0.0, height = 0.0
}
struct Rect {
	var origin = Point()
	var size = Size()
	var center: Point {
		get {
			let centerX = origin.x + (size.width / 2)
			let centerY = origin.y + (size.heigth / 2)
			return Point(x: centerX, y: centerY)
		}
		set (newCenter) {
			origin.x = newCenter.x - (size.width / 2)
			origin.y = newCenter.y - (size.heigth / 2)
		}
	}
}

var square = Rect(origin: Point(x: 0.0, y: 0.0),
					size: Size(width: 10.0, heigth: 10.0))
let intialSquareCenter = square.center
square.center = Point(x: 15, y: 15)
print("square.origin is now at (\\(square.origin.x), \\(square.origin.y))")
// Prints "square.origin is now at (10.0, 10.0)"

```

Если в `setter` не определено имя переменной, то используется имя по умолчанию - `newValue`.
