- Ключевое слово `var` 
```go
var x int = 10
var y = 10
var z int // z = 0
var a, b = 10, "hello"
```

	Declaration list
```go
var (
	x int
	y = 20
	z int = 30
	d,e = 40, "hello"
	f, g string
)
```

- `:=` оператор
```go
x := 10 // var x = 10
z, y := 10, "hello"
```
	`:=` нельзя использовать за пределами фнукций

- Ключевое слово `const`
	Constants in Go are a way to give names to literals. **They can only hold values that the compiler can figure out at compile time.**
```go
x := 1
y := 2
const z = x + y // x + y (value of type int) is not constant
```

>[!note]
There is no way in Go to declare that a variable is immutable.


