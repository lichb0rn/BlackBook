---
created: 2026-02-02
tags:
  - type/note
source: https://leetcode.com/problems/3sum/description/
related:
area:
up:
---
## Итерация 1

```go
func threeSum(nums []int) [][]int {
    data := slices.Sort(nums)
    result := int{}
    n := len(nums)

    for i := 0; i < n; i++ {
        target := -nums[i]

        // Решаем two sum на оставшихся числах
        left := i + 1
        right := n - 1
        for left < right {
            sum := nums[left] + nums[right]
            if sum < target {
                left += 1
                continue
            }

            if sum > target {
                right -= 1
                continue
            }

            if sum == target {
                result = append(result, int{target, left, right})
            }
        }
    }

    return result
}
```

Ошибки компиляции:
```
Line 2: Char 5: declared and not used: data (solution.go)
Line 2: Char 13: slices.Sort(nums) (no value) used as value (solution.go)
Line 3: Char 15: invalid composite literal type int (solution.go)
Line 25: Char 41: invalid composite literal type int (solution.go)
```

## Итерация 2
```go
func threeSum(nums []int) [][]int {
    data := slices.Sort(nums)
    result := []int{}
    n := len(nums)

    for i := 0; i < n; i++ {
        target := -data[i]

        // Решаем two sum на оставшихся числах
        left := i + 1
        right := n - 1
        for left < right {
            sum := data[left] + data[right]
            if sum < target {
                left += 1
                continue
            }

            if sum > target {
                right -= 1
                continue
            }

            if sum == target {
                result = append(result, []int{target, left, right})
            }
        }
    }

    return result
}
```

Снова ошибки компиляции:
```
Line 2: Char 13: slices.Sort(nums) (no value) used as value (solution.go)
Line 25: Char 41: cannot use []int{…} (value of type []int) as int value in argument to append (solution.go)
Line 30: Char 12: cannot use result (variable of type []int) as [][]int value in return statement (solution.go)
```

## Итерация 3
```go
func threeSum(nums []int) [][]int {
    slices.Sort(nums)
    result := [][]int{}
    n := len(nums)

    for i := 0; i < n; i++ {
        target := -nums[i]

        // Решаем two sum на оставшихся числах
        left := i + 1
        right := n - 1
        for left < right {
            sum := nums[left] + nums[right]
            if sum < target {
                left += 1
                continue
            }

            if sum > target {
                right -= 1
                continue
            }

            if sum == target {
                result = append(result, []int{target, left, right})
            }
        }
    }

    return result
}
```

Ошибка исполнения:
```
runtime/cgo: pthread_create failed: Resource temporarily unavailable
SIGABRT: abort
```

## Итерация 4
```go
func threeSum(nums []int) [][]int {
	slices.Sort(nums)

	n := len(nums)
	res := make([][]int, 0)

	for i := 0; i < n-2; i++ {
		// skip duplicates for i
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}

		// early stop: since sorted, if nums[i] > 0 no three numbers can sum to 0
		if nums[i] > 0 {
			break
		}

		left, right := i+1, n-1
		target := -nums[i]

		for left < right {
			sum := nums[left] + nums[right]

			if sum < target {
				left++
				continue
			}
			if sum > target {
				right--
				continue
			}

			// sum == target
			res = append(res, []int{nums[i], nums[left], nums[right]})

			left++
			right--

			// skip duplicates for left/right
			for left < right && nums[left] == nums[left-1] {
				left++
			}
			for left < right && nums[right] == nums[right+1] {
				right--
			}
		}
	}

	return res
}
```