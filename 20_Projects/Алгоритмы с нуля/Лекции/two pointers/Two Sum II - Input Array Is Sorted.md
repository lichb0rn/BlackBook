---
created: 2026-02-02
tags:
  - type/note
source: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/
related:
area:
up:
---
## Итерация 1
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum = target {
            return []int{left, right}
        }
    }
}
```

Ошибка компиляции: 
```
Line 16: Char 16: syntax error: cannot use assignment sum = target as value (solution.go)
```

## Итерация 2
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum == target {
            return []int{left, right}
        }
    }
}
```

Ошибка: 
```
Line 20: Char 1: missing return (solution.go)
```

## Итерация 3
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum == target {
            break
        }
    }
    return []int{left, right}
}
```

Решение неверное:
```
Input
numbers = [2,7,11,15]
target = 9

Output
[0,1]

Expected
[1,2]
```

## Итерация 4
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum == target {
            break
        }

        left += 1
        right -= 1
    }
    return []int{left, right}
}
```

Решение неверное:
```
Input
numbers = [2,7,11,15]
target = 9

Output
[0,1]

Expected
[1,2]
```

## Итерация 5
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            right -= 1
            continue
        }
        if sum > target {
            left += 1
            continue
        }

        if sum == target {
            break
        }

        left += 1
        right -= 1
    }
    return []int{left, right}
}
```

Решение неверное.

## Итерация 6
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            right -= 1
            continue
        }
        if sum > target {
            left += 1
            continue
        }

        if sum == target {
            break
        }
    }
    return []int{left, right}
}
```

## Итерация 7
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum == target {
            break
        }
    }
    return []int{left, right}
}
```

## Итерация 8
```go
func twoSum(numbers []int, target int) []int {
    left := 0
    right := len(numbers) - 1

    for left < right {
        sum := numbers[left] + numbers[right]
        if sum < target {
            left += 1
            continue
        }
        if sum > target {
            right -= 1
            continue
        }

        if sum == target {
            break
        }
    }
    return []int{left + 1, right + 1}
}
```

Решение правильное. Возвращаемые индексы должны быть +1, а не с нуля.