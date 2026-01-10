2021-03-06 13:05
Tags: #"" - [[iOS Development]] - [[Swift]]
\_\_

# discardableResult

`@discardableResult` перед функцией означает, что вызывающий код может игнорировать возвращаемое функцией значение.

## Код

```swift
@discardableResult func createItem() -> Item {
	let newItem = Item(random: true)
	allItems.append(newItem)
	return newItem
}

// This is OK
let newItem = itemStore.createItem()

// And that's OK too
itemStore.createItem()

```
