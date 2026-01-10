```go
if n == 0 {
	fmt.Println("Too low")
} else if n > 5 {
	fmt.Println("Too big: ", n)
} else {
	fmt.Println("Just right: ", n)
}
```

- Go adds is the ability to declare variables that are **scoped to the condition and to both the if and else blocks**.
```go
if n := rand.Intn(10); n == 0 {
	fmt.Println("Too low")
} else if n > 5 {
	fmt.Println("Too big: ", n)
} else {
	fmt.Println("Just right: ", n)
}
```

