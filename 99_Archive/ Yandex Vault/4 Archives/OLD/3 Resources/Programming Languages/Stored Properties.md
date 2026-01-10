2021-03-06 13:22
Tags: #"" - [[Swift Properties]] [[Swift]]
\_\_

# Stored properties

Самый простой тип свойств. Могу быть либо переменными (`var`), либо константами (`let`).

```swift
struct FixedLengthRange {
	var firstValue: Int
	let length: Int
}
```

`Stored` свойства могут быть ленивыми (`lazy`). В этом случае начальное значние не вычисляется до первого использования.
