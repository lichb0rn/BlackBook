---
uuid: 20220724195738
created: 2022-07-24T19:57:38
alias: dynamic import
---

# [[Async import]]

Для импорта модуля в runtime в [[ECMAScript modules|es]] есть специальный механизм - **dynamic imports**.

Async imports can be performed at runtime using the special `import()` operator. The `import()` operator is syntactically equivalent to a function that takes a module identifier as an argument and it returns a [[JavasScript Promises|promise]] that resolves to a module object.

```javascript
const SUPPORTED_LANGUAGES = ['el', 'en', 'es', 'it', 'pl']
const selectedLanguage = process.argv[2] 
if (!SUPPORTED_LANGUAGES.includes(selectedLanguage)) { 
	console.error('The specified language is not supported')
	process.exit(1)
}

const translationModule = `./strings-${selectedLanguage}.js`
import(translationModule)
	.then((strings) => {
		console.log(strings.HELLO)
	})
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[NodeJS Design Patterns]]