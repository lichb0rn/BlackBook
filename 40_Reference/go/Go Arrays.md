```go
var x [3]int // [0, 0, 0]
var y = [3]int{1,2,3}
var z = [...]int{1,2,3}
var xy [2][3]int
```

## Equality
```go
var x = [...]int{1,2,3}
var y = [3]int{1, 2, 3}
fmt.Println(x == y) // true
```

В [[Golang]] размер массива - часть его типа:

Go considers the size of the array to be part of the type of the array. This makes an array that’s declared to be `[3]int `a different type from an array that’s declared to be `[4]int`. 

This also means that you cannot use a variable to specify the size of an array, because types must be resolved at compile time, not at runtime.

What’s more, you can’t use a type conversion to directly convert arrays of different sizes to identical types. Because you can’t convert arrays of different sizes into each other, you can’t write a function that works with arrays of any size and you can’t assign arrays of different sizes to the same variable.

В [[Golang]] массивы используются в качестве хранилища для [[Go Slices]]