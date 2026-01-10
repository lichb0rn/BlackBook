---
uuid: 20220802154740
created: 2022-08-02T15:47:40
alias: 
- синхронный API
- асинхроинный API
---

# [[Synchronous vs Asynchronous API]]

Допустим у нас есть такая функция
```javascript
import { readFile } from 'fs'

const cache = new Map()

function inconsistentRead (filename, cb) {
	if (cache.has(filename)) {
		// invoked synchronously
		cb(cache.get(filename))
	} else {
		// asynchronous function
		readFile(filename, 'utf8', (err, data) => {
			cache.set(filename, data)
			cb(data)
		})
	}
}
```

Функция имеет непостоянное поведение:
- внутри блока `if === true`, если файл уже находится в кэше, то ответ будет синхронным
- внутри блока `if !== true` исполняется асинхронный код `readFile` из [[Node.js]].

Данная функция в различных обстоятельствах ведёт себя по-разному, что может вызвать трудно диагностируемые ошибки.

Есть два варианта исправления.

### Полностью синхронный API
```javascript
import { readFileSync } from 'fs'

const cache = new Map()

function consistentReadSync (filename) {
	if (cache.has(filename)) {
		return cache.get(filename)
	} else {
		const data = readFileSync(filename, 'utf8')
		cache.set(filename, data)
		return data
	}
}
```

В данном варианте асинхронный вариант чтения файла меняется на синхронный `readFileSync`.

Использовать синхронные варианты в [[Node.js]] не всегда возможно, т.к. в этом случае блокируется основной поток. 

### Асинхронный API
```javascript
import { readFile } from 'fs'

const cache = new Map()

function consistentReadAsync (filename, callback) {
	if (cache.has(filename)) {
		// deferred callback invocation
		process.nextTick(() => callback(cache.get(filename)))
	} else {
		// asynchronous function
		readFile(filename, 'utf8', (err, data) => {
			cache.set(filename, data)
			callback(data)
		})
	}
}
```

В этом варианте мы используем асинхронную версию чтения из файла `readFile`, а ответ из кэша откладываем до следующего цикла [[Node.js]] с помощью `process.nextTick(() => callback())`

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note