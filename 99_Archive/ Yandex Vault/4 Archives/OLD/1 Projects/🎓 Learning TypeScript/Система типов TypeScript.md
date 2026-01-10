---
uuid: 20230905203054
created: 2023-09-05T20:30:54
aliases:
  - typescript types
  - typescript type system
---

# [[Система типов TypeScript]]

## Основные типы
[[TypeScript any type|Тип any]]
[[TypeScript unknown type|Тип unknown]]
[[TypeScript boolean type|Тип boolean]]
[[TypeScript number type|Тип number]]
[[TypeScript bigint|Тип bigint]]
[[TypeScript string|Тип string]]
[[TypeScript symbol|Тип symbol]]
[[TypeScript object|Тип object]]
[[TypeScript array|Массивы]]
[[TypeScript tuples|Кортежи]]
[[TypeScript null types]]
[[TypeScript enum|Перечисления]]
[[TypeScript Generics|Обобщенные типы]]

## Псевдонимы и пересечения типов
- Псевдонимы типов
	- `type Age = number`
	- `type Person = { name: string, age: Age }`
	- псевдоним типы всегда можно заменить типом, на который он указывает
	- переопределить псевдоним нельзя
	- так же как для `let` и `const`, диапазон псевдонимов типов ограничен одним блоком
	- внутренние объявления псевдонимов типов перекрывают внешние:
```ts
type Color = 'red';
let x = Math.random() %3C 0.5;
if (x) {
    type Color = 'blue';
    let b: Color = 'blue';
} else {
    let c: 'red';
}
```

## Типы объединения и пересечения
[[TypeScript]] предоставляет специальные операторы типов для описания объединений и пересечений: `|` для объединения и `&` для пересечения.
```ts
type Cat = { name: string; purrs: boolean };
type Dog = { name: string; barks: boolean; wags: boolean };
type CatOrDogorBoth = Cat | Dog;
type CatAndDog = Cat & Dog;

// Cat
let catOrDog: CatOrDogorBoth = {
	name: 'Bonkers',
	purrs: true,
};
// Dog
catOrDog = {
	name: 'Domino',
	barks: true,
	wags: true,
};
// Both
catOrDog = {
	name: 'Donkers',
	barks: true,
	wags: true,
	purrs: true,
};
let catAndDog: CatAndDog = {
	name: 'Domino',
	barks: true,
	purrs: true,
	wags: true,
};
```

Или в возврате из функции:
```ts
function trueOrNull(isTrue: boolean): string | null {
	if (isTrue) return 'true';
	return null;
}
```
## Неизменяемые массивы и кортежи
```ts
let as: readonly number[] = [1, 2, 3]
```
Также можно использовать более длинные формы объявления:
```ts
type A = readonly string[]
type B = ReadonlyArray<string>
type C = Readonly<string[]>

type D = readonly [number, string]
type E = Readonly<[number, string]>
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Профессиональный TypeScript]]
- 🏷️ Tags:: [[TypeScript]], [[Type Systems]]