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
func findMaxAverage(nums []int, k int) float64 {
    begin := 0
    windowState

    for end := range len(nums) {
        windowSize := end - begin + 1

        if // window condition {
            begin++ // shrink window
        }
    }    
}
```