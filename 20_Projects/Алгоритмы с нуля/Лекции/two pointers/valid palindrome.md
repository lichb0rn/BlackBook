---
created: 2026-02-02
tags:
  - type/note
source: https://leetcode.com/problems/valid-palindrome/
related:
area:
up:
---

## Итерация 1 
```go
func isPalindrome(s string) bool {
    func isAlphaNumeric(c byte) bool {
        if (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9') {
            return true
        }
        return false
    }

    start := 0
    end := len(s) - 1

    for start < end {
        left := strings.ToLower(s[start])
        right := strings.ToLower(s[end])

        if(!isAlphaNumeric(left)) {
            start += 1
            continue    
        }

        if(!isAlphaNumeric(right)) {
            end -= 1
            continue
        }

        if left != right {
            return false
        }

        start += 1
        end -= 1
    }
    return true
}
```

Получил ошибку: 
```
Line 2: Char 10: syntax error: unexpected name isAlphaNumeric, expected ( (solution.go)
```

## Итерация 2
```go
func isPalindrome(s string) bool {
    start := 0
    end := len(s) - 1

    for start < end {
        left := strings.ToLower(s[start])
        right := strings.ToLower(s[end])

        if(!isAlphaNumeric(left)) {
            start += 1
            continue    
        }

        if(!isAlphaNumeric(right)) {
            end -= 1
            continue
        }

        if left != right {
            return false
        }

        start += 1
        end -= 1
    }
    return true
}

func isAlphaNumeric(c byte) bool {
    if (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9') {
        return true
    }
    return false
}
```

 Снова ошибки компиляции:
```
Line 6: Char 33: cannot use s[start] (value of type byte) as string value in argument to strings.ToLower (solution.go)
Line 7: Char 34: cannot use s[end] (value of type byte) as string value in argument to strings.ToLower (solution.go)
Line 9: Char 28: cannot use left (variable of type string) as byte value in argument to isAlphaNumeric (solution.go)
Line 14: Char 28: cannot use right (variable of type string) as byte value in argument to isAlphaNumeric (solution.go) 
```

## Итерация 3
```go
func isPalindrome(s string) bool {
    start := 0
    end := len(s) - 1

    str := strings.ToLower(s)

    for start < end {
        left := str[start]
        right := str[end]

        if(!isAlphaNumeric(left)) {
            start += 1
            continue    
        }

        if(!isAlphaNumeric(right)) {
            end -= 1
            continue
        }

        if left != right {
            return false
        }

        start += 1
        end -= 1
    }
    return true
}

func isAlphaNumeric(c byte) bool {
    if (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9') {
        return true
    }
    return false
}
```

Ошибок нет, решение принято.


