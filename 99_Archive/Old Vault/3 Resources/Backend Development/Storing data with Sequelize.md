---
uuid: 20220627121023
created: 2022-06-27T12:10:23
alias: sequelize
tags: 
---

# [[Storing data with Sequelize]]

MOC:  [[063 Frameworks]]

---

Сохранять данные [[Discord]] бота можно в [[sqlite]] c помощью sequelize.

## Установка 
````
npm install discord.js sequelize sqlite3
````

## Инициализация
```js
const Sequelize = require('sequelize');

const sequelize = new Sequelize('database', 'user', 'password', {
	host: 'localhost',
	dialect: 'sqlite',
	logging: false,
	// SQLite only
	storage: 'database.sqlite',
});```

## Создание модели
```js
/*
 * equivalent to: CREATE TABLE tags(
 * name VARCHAR(255) UNIQUE,
 * description TEXT,
 * username VARCHAR(255),
 * usage_count  INT NOT NULL DEFAULT 0
 * );
 */
const Tags = sequelize.define('tags', {
	name: {
		type: Sequelize.STRING,
		unique: true,
	},
	description: Sequelize.TEXT,
	username: Sequelize.STRING,
	usage_count: {
		type: Sequelize.INTEGER,
		defaultValue: 0,
		allowNull: false,
	},
});
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [Discord.js](https://discordjs.guide/sequelize/#adding-a-tag)