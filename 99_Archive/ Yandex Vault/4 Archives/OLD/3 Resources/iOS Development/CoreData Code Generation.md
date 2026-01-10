---
aliases: [""]
---
MOC:  [[Core Data]]

__
# Генерация кода в Core Data
После определения entities, атрибутов и связей, необходимо создать классы для управления объектами Core Data. Core Data опционально может создать файл класса и файл свойств.

Файл класса объявляет класс подклассом от [[NSManagedObject]]:
```swift
import Foundation
import CoreData

@objc(Quake)
public class Quake: NSManagedObject {

}
```

Файл свойств объявляет `extension`, в котором хранятся `@NSManaged` свойства, представляющие атрибуты модели и связи, а также дополнительная функциональность.

Существует 3 варианта генерации кода в Core Data:
- Manual/None
- Class Definition
- Category/Extension

## Manual/None

## Class Definition

## Category/Extension