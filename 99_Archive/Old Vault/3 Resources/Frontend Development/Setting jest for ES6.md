---
uuid: 20220801094240
created: 2022-08-01T09:42:40
alias: настройка jest для es6 модулей
---

# [[Setting jest for ES6]]

Чтобы в [[Jest]] заработали импорты [[Exports in ESM]] нужно:

1. Ставим [[babel]]: `npm install --save-dev babel-jest`
2. В `package.json` прописываем:
```javacript
{ "scripts": 
	{ "test": "jest" }, 
	"jest": { 
		"transform": { 
			"^.+\\.[t|j]sx?$": "babel-jest" 
		} 
	} 
}
```

3. Создаём `babel.config.json`:
- `npm install @babel/preset-env --save-dev`
- в `babel.config.json` пишем:
```javascript
{ 
	"presets": ["@babel/preset-env"] 
}
```

После чего можно использовать:
`ship.js`:
```javascript
class Ship {
	constructor(length) {
		this.length = length;
	}
}
export { Ship };
```

`ship.test.js`:
```javascript
import { Ship } from '../src/ship';

test('test battleship initialization with length 2', () => {
	const ship = new Ship(2);
	expect(ship.length).toBe(2);
});
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note