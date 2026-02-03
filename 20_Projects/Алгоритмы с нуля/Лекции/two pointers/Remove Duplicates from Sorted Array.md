---
created: 2026-02-03
tags:
  - type/note
source: https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/
related:
area:
up:
---
## Итерация 1
```go
func removeDuplicates(nums []int) int {
    p := 0
    for i := range len(nums) {
        if nums[p] != nums[i] {
            p += 1
            nums[p] = nums[i]
        }
    }
    return p + 1
}
```

