2021-03-06 13:48
Tags: #"" - [[Swift Properties]] - [[Swift]]
\_\_

# Property wrappers

`Property wrapper` добавляет слой разделения между кодом, который описывает хранение свойства, и кодом, отвечающим за управление свойтсвом.

Для определения `property wrapper` необходимо опеределить [[Swift Structures|структуру]], [[Swift Enumeration|перечисление]] или [[Swift Class|класс]].

В коже ниже структура `TwelveOrLess` гарантирует, что значение всегда содержит числе <= 12. При попытке сохранить значение бОльшее значние, будет сохранено 12:

```swift
@propertyWrapper
struct TwelveOrLess {
	private var number: Int
	init() { self.number = 0 }
	var wrappedValue: Int {
		get { return number }
		set { number = min(newValue, 12) }
	}
}
```

Применение:

```swift
struct SmallRectangle {
	@TwelveOrLess var height: Int
	@TwelveOrLess var width: Int
}

var rectangle = SmallRectangle()
print(rectangle.height)
// Prints "0"

rectangle.height = 10
print(rectangle.height)
// Prints "10"

rectangle.height = 24
print(rectangle.height)
// Prints "12"
```
