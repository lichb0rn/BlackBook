```go
var x = []int{1, 2, 3}
```

> [!note]
> `[...]` - создание массива, `[]` - slice

Default zero value для слайса - `nil`

## Append
```go
var s []int
fmt.Println(s) // []
s = append(s, 1, 2, 3)
fmt.Println(s) // [1 2 3]
```

>[!note]
> It is a compile-time error if you forget to assign the value returned from append.

>[!note]
> [[Golang]] is a **call-by-value** language. Every time you pass a parameter to a function, Go makes a copy of the value that’s passed in. Passing a slice to the append function actually passes a copy of the slice to the function.

## Capacity
Слайсы в [[Golang]] - аналог [[Dynamic Array|динамических массивов]]
