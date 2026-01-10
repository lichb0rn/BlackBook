2021-03-06 15:24
Tags: #"" - [[Swift]] - [[Swift Foundation]]
\_\_

# NSAttributedString

[[Swift Class|Класс]] предназачен для декорирования строк в [[Swift Foundation]].
С его помощью раскаршивать отдельные элементы [[Swift Strings|строк]], вставлять ссылки и изображения.

## Создание attributed строки

```swift
let quote = "Haters gonna hare"
let attributedQuote = NSAttributedString(sttring: quote)
```

Без добавления атрибутов [[NSAttributedString]] выглядит как обычная строка.

## Декорирования attributed строки

```swift
let quote = "Haters gonna hate"
let font = UIFont.systemFont(ofSize: 72)
let attributes = [NSAttributedString.Key.font: font]
let attributedQuote = NSAttributedString(string: quote, attributes: attributes)
```

Теперь будет отображен текст с шрифтом 72 размера.

Можно добавить цвет и свечение:

```swift
let font = UIFont.systemFont(ofSize: 72)
let shadow = NSShadow()
shadow.shadowColor = UIColor.red
shadow.shadowBlurRadius = 5

let attributes: [NSAttributedString.Key: Any] = [
    .font: font,
    .foregroundColor: UIColor.white,
    .shadow: shadow
]
```

## Добавление изображения

Для начала создаём обычную [[NSMutableAttributedString]]:

```swift
let fullString = NSMutableAttributedString(string: "Your rank: ")

```

Далее создаём экземпляр [[NSTextAttachment]]:

```swift
let image1Attachment = NSTextAttachment()
image1Attachment.image = UIImage(named: "rank-major.png")
```

Оборачиваем [[NSTextAttachment]] в [[NSAttributedString]]:

```swift
let image1String = NSAttributedString(attachment: image1Attachment)
```

И добавялем в строке:

```swift
fullString.append(image1String)
```

## Web-ссылки в attributed строке

Ссылки - всего лишь атрибут, определяемый `NSAttributedString.Key.link`

```swift
let attributedString = NSMutableAttributedString(string: "Want to learn iOS? You should visit the best source of free iOS tutorials!")
attributedString.addAttribute(.link, value: "https://www.hackingwithswift.com", range: NSRange(location: 19, length: 55))
```

\_\_

### External Links

- [HackingWithSwift](https://www.hackingwithswift.com/articles/113/nsattributedstring-by-example)
- [Apple Docs](https://developer.apple.com/documentation/foundation/nsattributedstring)
