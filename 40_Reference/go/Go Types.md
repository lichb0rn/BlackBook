[[Golang]] присваивает нулевое значение по умолчанию всем объявленным, но неинициализированным переменным.

- Integers
	```go
int8
int16
int32
int64
uint8
uint16
uint32
uint64

int
uint
```
- `byte`  - алиас для `uint8`
- `int` - `int32` для 32-битных CPU, `int64` - для 64-битных.

- Floats
```go
float32
float64
```

- Complex
```go
complex64
complex128

var complexNum = complex(20.3, 10.2)
```

- Strings and runes
```go
var char rune = 'J'
var str = 'hello world'
```


## Type conversion
```go
var x int = 10
var y float64 = 30.2
var sum1 float64 = float64(x) + y
var sum2 int = x + int(y)
fmt.Println(sum1, sum2)
```