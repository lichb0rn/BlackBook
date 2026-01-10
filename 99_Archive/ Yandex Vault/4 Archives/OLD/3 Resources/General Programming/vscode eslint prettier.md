---
uuid: 20220730084634
created: 2022-07-30T08:46:34
alias: code formatting
---

# [[vscode eslint prettier]]

1. Ставим пакеты
```node
npm i -D eslint prettier eslint-plugin-prettier eslint-config-prettier eslint-plugin-node eslint-config-node
```

```javascript
npx install-peerdeps --dev eslint-config-airbnb
```

2. Создаём конфиги
- `.prettierrc`:
```javascript
{
	"singleQuote": true,
	"arrowParens": "avoid",
	"tabWidth": 2,
	"useTabs": false,
	"printWidth": 100,
	"proseWrap": "always",
	"bracketSpacing": false,
	"trailingComma": "es5"
}
```
- `eslinit --init`:
```javascript
{
	"extends": ["airbnb", "prettier", "plugin:node/recommended"],
	"plugins": ["prettier"],
	"rules": {
		"prettier/prettier": "error",
		"no-unused-vars": "warn"
	}
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note