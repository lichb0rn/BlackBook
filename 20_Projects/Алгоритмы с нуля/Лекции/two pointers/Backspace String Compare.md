---
created: 2026-02-03
tags:
  - type/note
source: https://leetcode.com/problems/backspace-string-compare/
related:
area:
up:
---
- [ ] #task Решить задачу [[Backspace String Compare]] ⏳ 2026-02-04

## Итерация 1
```go
func backspaceCompare(s string, t string) bool {
    n := len(s) - 1
    m := len(t) - 1

    skip_s := 0
    skip_t := 0

    for n >= 0 && m >= 0 {
        // ToDo: implement skip
        // if # or skip_counter > 0
        if s[n] == "#" {
            skip_s += 1
        }
        n -= skip_s
        
        if t[m] == "#" {
            skip_t += 1
        }
        m -= skip_t


        if s[n] != s[m] {
            return false
        }

        n -= 1
        m -= 1
    }
    return n == m
}
```

## Итерация 2
```go
func backspaceCompare(s, t string) bool {
	i, j := len(s)-1, len(t)-1
	skipS, skipT := 0, 0

	for i >= 0 || j >= 0 {
		for i >= 0 {
			if s[i] == '#' {
				skipS++
				i--
			} else if skipS > 0 {
				skipS--
				i--
			} else {
				break
			}
		}

		for j >= 0 {
			if t[j] == '#' {
				skipT++
				j--
			} else if skipT > 0 {
				skipT--
				j--
			} else {
				break
			}
		}

		if i >= 0 && j >= 0 {
			if s[i] != t[j] {
				return false
			}
		} else {
			if i >= 0 || j >= 0 {
				return false
			}
		}

		i--
		j--
	}

	return true
}
```