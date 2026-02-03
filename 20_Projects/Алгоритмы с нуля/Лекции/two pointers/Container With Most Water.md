---
created: 2026-02-03
tags:
  - type/note
source: https://leetcode.com/problems/container-with-most-water/description/
related:
area:
up:
---
## Итерация 1
```go
func maxArea(height []int) int {
    // на каждой итерации
    // result = max(result, ...)
    left := 0
    right := len(height) - 1

    result := 0

    for left < right {
        width := right - left
        square := width * min(height[left], height[right])
        result = max(result, square)

        if height[left] < height[right] {
            left += 1
        } else {
            right += 1
        }
    }

    return result
}

func max(a, b int) int {
    if a > b {
        return a
    } else {
        return b
    }
}

func min(a, b int) int {
    if a < b {
        return a
    } else {
        return b
    }
}
```

Ошибка:
```
panic: runtime error: index out of range [9] with length 9
main.maxArea({0xc0001b0000?, 0x13?, 0x18?})
solution.go, line 11
main.__helper__(...)
solution.go, line 43
main.main()
solution.go, line 73
```


## Итерация 2
```go
func maxArea(height []int) int {
    // на каждой итерации
    // result = max(result, ...)
    left := 0
    right := len(height) - 1

    result := 0

    for left < right {
        width := right - left
        square := width * min(height[left], height[right])
        result = max(result, square)

        if height[left] < height[right] {
            left += 1
        } else {
            right -= 1
        }
    }

    return result
}

func max(a, b int) int {
    if a > b {
        return a
    } else {
        return b
    }
}

func min(a, b int) int {
    if a < b {
        return a
    } else {
        return b
    }
}
```

Ошибка была в том, что не в ту сторону двигал `right`.