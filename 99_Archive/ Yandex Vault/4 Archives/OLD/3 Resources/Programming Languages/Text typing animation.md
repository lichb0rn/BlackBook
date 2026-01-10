2021-03-06 12:56
Tags: #"" - [[UIKit]] - [[iOS Development]]
\_\_

# Text typing animation

Анимация ввода текста в [[UILabel]]

## Код

```swift
titleLabel.text = ""
var characterIndex = 0.0
let titleText = "Some text"
for letter in titleText {
	Timer.scheduledTimer((withTimeInterval: 0.1 \* characterIndex, repeats: false) { (timer) in
		self.titleLabel.text?.append(letter)
	}
	characterIndex += 1
}
```

1. Обнуляем [[UILabel]]
2. `characterIndex` - задержка в зависимости от позиции буквы
