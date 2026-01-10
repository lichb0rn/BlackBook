```go
type person struct {
	name string
	age int
	pet string
}

var fred person
bob := person{}
julia := person{
	"Julia",
	40,
	"cat"
}
beth := person{
	age: 30,
	name: "Beth"
}

bob.name = "Bob"
fmt.Println(bob.name)
```

Структуры можно определять внутри и снаружи [[Go Function|функции]]. Структура, определённая внутри функции, может быть использована только внутри функции.

## Anonymous structs
```go
pet := struct {
	name string
	kind string
} {
	name: "Fido",
	kind: "dog"
}
```

Anonymous structs are handy in two common situations. The first is when you translate external data into a struct or a struct into external data (like JSON or Protocol Buffers). This is called **unmarshaling** and **marshaling** data, respectively.