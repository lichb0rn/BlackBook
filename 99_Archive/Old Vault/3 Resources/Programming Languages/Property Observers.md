2021-03-06 13:37
Tags: #"" - [[Swift]] - [[Swift Properties]]
\_\_

# Property observers

`Property observers` отслеживают и реагируются на изменения в значении свойства. Они вызываются каждый раз при изменении значения свойтсва даже, если новое значение такое же, как и было.
`Property observers` можно добавить:

- к явно пределенным [[Stored Properties]]
- к унаследованным [[Stored Properties]]
- к унаследованным [[Computed Properties]]

Можно определить одно или оба наблюдателей:

- `willSet` вызывается перед изменением значения свойства
- `didSet` вызывается сразу после изменения значения

```swift
class StepCounter {
	var totalSteps: Int = 0 {
		willSet(newTotalSteps) {
			print("Setting totalSteps to \(newTotalSteps)")
		}
		didSet {
			if totalSteps > oldValue {
			print("Added \(totalSteps - oldValue) steps")
			}
		}
	}
}

let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps

stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps

stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps

```
