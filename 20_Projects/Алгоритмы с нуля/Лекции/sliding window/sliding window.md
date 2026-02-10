---
created: 2026-02-10
tags:
  - type/note
source:
related:
area: "[[Computer Science]]"
up:
  - "[[Алгоритмы с нуля]]"
aliases:
  - скользящее окно
---
![[Pasted image 20260210082600.png]]

## Каркас решения задач
 ```go
func minSubArrayLen(target int, nums []int) int {
    begin := 0
    windowState
    result

    for end := range len(nums) {
        windowState
        windowSize := end - begin + 1

        if // window condition {
            result
            windowState
            begin++ // shrink window
        }
    }     
}
```