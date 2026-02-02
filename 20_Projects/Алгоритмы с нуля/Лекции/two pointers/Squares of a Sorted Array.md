---
created: 2026-02-02
tags:
  - type/note
source: https://leetcode.com/problems/squares-of-a-sorted-array/description/
related:
area:
up:
---
## Итерация 1
```go
func sortedSquares(nums []int) []int {
    n := len(nums)
    left := 0
    right := n - 1
    res := make([]int, n)

    for i, _ := slices.Backwards(res) {
        leftSq := nums[left] * nums[left]
        rightSq := nums[right] * nums[right]

        if leftSq < rightSq {
            res[i] = rightSq
            right -= 1
        } else {
            res[i] = leftSq
            left += 1
        }
    }

    return res
}
```

Ошибка компиляции: `Line 7: Char 14: syntax error: cannot use i, _ := slices.Backwards(res) as value (solution.go)`

## Итерация 2
```go
func sortedSquares(nums []int) []int {
    n := len(nums)
    left := 0
    right := n - 1
    res := make([]int, n)

    for i, _ := range slices.Backward(res) {
        leftSq := nums[left] * nums[left]
        rightSq := nums[right] * nums[right]

        if leftSq < rightSq {
            res[i] = rightSq
            right -= 1
        } else {
            res[i] = leftSq
            left += 1
        }
    }

    return res
}
```