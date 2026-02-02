---
created: 2026-02-02
tags:
  - type/note
source: https://leetcode.com/problems/reverse-string/description/
related:
area:
up:
---
Правильное решение

```go
func reverseString(s []byte)  {
    left := 0
    right := len(s) - 1

    for left < right {
        s[left],s[right] = s[right], s[left]
        left += 1
        right -= 1
    }
}
```