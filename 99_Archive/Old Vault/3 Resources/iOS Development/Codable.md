---
uuid: 20221201093939
created: 2022-12-01T09:39:39
alias: codable
---

# [[Codable]]

`Codable` - протокол, который состоит из двух других протоколов: [[Encodable]], [[Decodable]]

## CodingKeys
[[CodingKey]] - протокол, описывающий, как `key` представлен:
```swift
public protocol CodingKey {
  var stringValue: String { get }
  var intValue: Int? { get }

  init?(stringValue: String)
  init?(intValue: Int)
}
```

## Custom CodingKey
Пример кастомного `codingKey` для преобразования из `kebab-case` в `camelCase`.

```swift
extension JSONDecoder.KeyDecodingStrategy {
    struct AnyCodingKey: CodingKey {
        let stringValue: String
        let intValue: Int?
        
        init?(stringValue: String) {
            self.stringValue = stringValue
            self.intValue = nil
        }
        
        init?(intValue: Int) {
            self.intValue = intValue
            self.stringValue = "\(intValue)"
        }
    }
    
    static var convertFromKebabCase: JSONDecoder.KeyDecodingStrategy = .custom { keys in
        print(keys)
        let codingKey = keys.last!
        let key = codingKey.stringValue
        
        guard key.contains("-") else { return codingKey }
        
        let words = key.components(separatedBy: "-")
        let camelCased = words[0] + words[1...].map(\.capitalized).joined()
        
        return AnyCodingKey(stringValue: camelCased)!
    }
}
```

## Containers
Существуют 3 типа контейнеров:
- **Keyed Container** - декодирование словаря, *ключами* которого являются CodingKeys.
- **Unkeyed Container** - используется для декодирования структур, у которого нет строковых ключей (например, массивы).
- **Single Value Container** - используется для декодирования одного значения в конкретный тип.
![[Pasted image 20221201122702.png]]

Контейнеры могут быть вложенными (nested).

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]
-  🏷️ Tags:: [[Swift]]