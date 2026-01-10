```go
for i := 0; i < 10; i++ {
	fmt.Println(i)
}

for i := 0; i < 10; {
	fmt.Println(i)
	if i % 2 == 0 {
		i++
	} else {
		i+=2
	}
}
```

## Condition only for statement

```go
i := 1
for i < 100 {
	fmt.Println(i)
	i = i * 2
}
```

## Infinit loop

```go
for {
	fmt.Println("hello")
}
```

### do-while analogue

```go
for {
	if !CONDITION {
		break
	}
}
```

## for-range

```go
evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
	fmt.Println(i, v)
}
```