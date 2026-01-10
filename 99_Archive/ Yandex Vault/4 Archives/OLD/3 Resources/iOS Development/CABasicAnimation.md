---
uuid: 20220921065847
created: 2022-09-21T06:58:47
alias:
---

# [[CABasicAnimation]]

An object that provides basic, single-keyframe animation capabilities for a layer property.

```swift
let flyRight = CABasicAnimation(keyPath: "position.x")
flyRight.fromValue = -view.bounds.size.width / 2
flyRight.toValue = view.bounds.size.width / 2
flyRight.duration = 0.5

heading.layer.add(flyRight, forKey: nil)
```

- A `CABasicAnimation` - объектная модель, не привязанная к конкретному [[CALayer|layer]].
- `add(_:forKey:)` создаёт копию модели.

## Animations vs. real content

Допустим мы уберём `fromValue` из кода выше и разместим  [[UIView|view]] вот так:
```swift
let flyRight = CABasicAnimation(keyPath: "position.x")
flyRight.toValue = view.bounds.size.width / 2
flyRight.duration = 0.5

username.layer.position.x -= view.bounds.width
password.layer.position.x -= view.bounds.width

flyRight.beginTime = CACurrentMediaTime() + 0.3
username.layer.add(flyRight, forKey: nil)
flyRight.beginTime = CACurrentMediaTime() + 0.4
password.layer.add(flyRight, forKey: nil)
```

По завершению анимации оба `view`  пропадут с экрана:
>[!quote] [[iOS Animations by Tutorials]]
>When you animate a layer, you’re not actually seeing the layer itself animated; instead, you’re seeing a cached version of it known as the **presentation layer**. The presentation layer is removed from the screen once the animation completes and the original layer shows itself again.

`presentation layer` можно оставить на экране, установив `flyRight.isRemovedOnCompletion = false`. Данная опция оставляет анимацию на экране, но
>[!quote] [[iOS Animations by Tutorials]]
> Although you know how `isRemovedOnCompletion` works when set to false, try to avoid it whenever possible. **Leaving animations on the screen affects performance**, so you’ll let them be removed automatically and update the original layer’s position instead.

## Ссылка на анимацию
 Метод `add` у [[CALayer]] имеет следующие параметры:
 ```swift
 func add(
    _ anim: CAAnimation,
    forKey key: String?
)```
`anim` - анимация
`forKey` - строка, которая идентифицирует анимацию

Например, у нас есть появляющийся справа элемент
```swift
let flyLeft = CABasicAnimation(keyPath: "position.x")
flyLeft.fromValue = info.layer.position.x + view.frame.size.width
flyLeft.toValue = info.layer.position.x
flyLeft.duration = 5.0
info.layer.add(flyLeft, forKey: "infoappear")
```

Где-нибудь в коде, мы захотим убрать анимацию:
```swift
info.layer.removeAnimation(forKey: "infoappear")
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note