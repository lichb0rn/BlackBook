---
uuid: 20230202181256
created: 2023-02-02T18:12:56
alias:
- currying
- каррирование
---

# [[Currying]]

Каррирование – продвинутая техника для работы с функциями. Она используется не только в [[JavaScript]], но и в других языках.

Каррирование – это трансформация функций таким образом, чтобы они принимали аргументы не как `f(a, b, c)`, а как `f(a)(b)(c)`.

Каррирование не вызывает функцию. Оно просто трансформирует её.

## Пример
Допустим, у нас есть код на [[Swift]]:
```swift
func aHigherOrderFunction(_ operation: (Int) -> () ) {
    let numbers = 1...10
    numbers.forEach(operation)
}

func someOperation(_ p1: Int, _ p2: String) {
    print("Number is: \(p1), string is: \(p2)")
}

aHigherOrderFunction { someOperation($0, "a constant") }
```

Чтобы преобразовать в функцию, которая принимает только один параметр, начнём с изменения сигнатуры: `func curried_SomeOperation(_ p1: Int) -> (String) -> ()`:
```swift
func curried_SomeOperation(_ p1: Int) -> (String) -> () {
    return { str in
        print("Number is: \(p1), string is: \(str)")
    }
}
```

Всё работает: `aHigherOrderFunction { curried_SomeOperation($0)("a constant") }`
Чтобы убрать closure, нужно поменять порядок параметров: `func curried_SomeOperation(_ str: String) -> (Int) -> ()`:
```swift
func curried_SomeOperation(_ str: String) -> (Int) -> () {
    return { p1 in
        print("Number is: \(p1), string is: \(str)")
    }
}
aHigherOrderFunction { curried_SomeOperation("a constant")($0) }
```

Теперь, когда строка идёт первой, функция `curried_SomeOperation` возвращает функцию, которую ожидает `aHigherOrderFunction`, и мы можем спокойно убрать замыкание: `aHigherOrderFunction(curried_SomeOperation("a constant"))`

## Generic currying
[[Swift Generics|Generic]] функция для каррирования:
```swift
func curry<A, B, C>(
    _ originalMethod: @escaping (A, B) -> C
) -> (A) -> (B) -> C {
    return { a in
        { b in
            originalMethod(a, b)
        }
    }
}
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[https://learn.javascript.ru/currying-partials]], [[Expert Swift]]
-  🏷️ Tags:: [[040 Computer Science]], [[020 Math|Math]]