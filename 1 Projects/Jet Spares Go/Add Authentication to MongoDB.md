---
up:
  - "[[MongoDB]]"
related: "[[Jet Spares]]"
created: 2025-04-20
---
Чтобы включить [[Аутентификация|аутентификацию]] на уже работающей в продуктиве [[MongoDB]]:
1. Зайти в БД и создать пользователя 
```js
use admin;
db.createUser({
  user: "root",
  pwd: "example",
  roles: [ { role: "root", db: "admin" } ]
});
```

Можно также создать отдельного пользователя для конкретной БД:
```js
use spares;
db.createUser({
  user: "appuser",
  pwd: "apppassword",
  roles: [ { role: "readWrite", db: "spares" } ]
});
```

2. Прописываем переменные окружения в [[Docker Compose|compose]] файле:
```yaml
db:
	container_name: mongodb
	image: mongo:latest
	ports:
		- 27017:27017
	volumes:
		- spares:/data/spares
	environment:
		MONGO_INITDB_ROOT_USERNAME: ${MONGO_INITDB_ROOT_USERNAME}
		MONGO_INITDB_ROOT_PASSWORD: ${MONGO_INITDB_ROOT_PASSWORD}
```

3. Добавить переменные окружения:
```sh
MONGO_INITDB_ROOT_USERNAME=root
MONGO_INITDB_ROOT_PASSWORD=password
APP_DB_NAME=spares
APP_USER=jetspares
APP_PASSWORD=jetspares

FRONTEND_VERSION=1.3.3
API_VERSION=1.4.2
EXPORT_VERSION=1.0.1
IMPORT_VERSION=1.0.0
```

