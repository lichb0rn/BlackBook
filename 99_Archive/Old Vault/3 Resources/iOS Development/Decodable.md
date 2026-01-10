---
uuid: 20221201094048
created: 2022-12-01T09:40:48
alias: decodable
---

# [[Decodable]]

Протокол для декодирования данных, например, [[JSON]].

### Полезные свойства
- декодирование `snake_case`:
```swift
decoder.keyDecodingStrategy = .convertFromSnakeCase
// store_link -> storeLink
```

- декодирование [[Swift Data]]:
```swift
decoder.dataDecodingStrategy = .base64

struct SomeModel {
	let imageBlob: Data
	var image: UIImage? { UIImage(data: imageBlob) }
}
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
-  🏷️ Tags:: [[Swift]]