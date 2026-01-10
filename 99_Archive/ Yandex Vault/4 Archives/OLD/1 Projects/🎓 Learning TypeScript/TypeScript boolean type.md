---
uuid: 20230906200922
created: 2023-09-06T20:09:22
aliases:
  - boolean
---

# [[TypeScript boolean type]]

Тип `boolean` (логический) имеет всего два значения: `true` и `false`. Такие типы можно сравнивать `(==, ===, ||, && и ?)` и отрицать (`!`). Используются они так:

```ts
let a = true             // boolean
var b = false            // boolean
const c = true           // true 
let d: boolean = true    // boolean 
let e: true = true       // true
let f: true = false   // Ошибка TS2322: тип 'false' не может быть 
				// присвоен типу 'true'.

```

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source::  [[Профессиональный TypeScript]]
- 🏷️ Tags::  [[Система типов TypeScript]]