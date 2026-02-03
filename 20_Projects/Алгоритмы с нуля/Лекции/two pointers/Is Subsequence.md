---
created: 2026-02-03
tags:
  - type/note
source: https://leetcode.com/problems/is-subsequence/description/
related:
area:
up:
---
## Итерация 1
```go
func isSubsequence(sub string, s string) bool {
    p1 := 0
    p2 := 0

    for p1 < len(sub) && p2 < len(s) {
        if sub[p1] == s[p2] {
            p1 += 1
        }
        p2 += 1
    }

    return p1 == len(sub)
}
```

