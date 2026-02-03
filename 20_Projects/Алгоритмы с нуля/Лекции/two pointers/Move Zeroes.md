---
created: 2026-02-03
tags:
  - type/note
source: https://leetcode.com/problems/move-zeroes/description/
related:
area:
up:
---
## Итерация 1
```go
func moveZeroes(nums []int)  {
    p := 0
    for i := range len(nums) {
        if nums[i] != 0 {
            nums[p], nums[i] = nums[i], nums[p]
            p += 1
        }
    }
}
```

Идея в том, что у нас `i` - указатель на нули, а `p` - на ненулевые данные.
Мы идём по массиву, пока встретим не ноль. Как только встретили - меняем местами.