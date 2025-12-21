---
tags:
  - type/note
domain: "[[Разработка web-приложений на Go|Go web development]]"
topics:
sources:
---
# Структура БД и пароли SnippetBox

## Доступы
- root@localhost:3306 / password
- web@localhost:3306 / password

## Структура БД

```sql
CREATE TABLE `snippets` (
  `id` int NOT NULL AUTO_INCREMENT,
  `title` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL,
  `content` text COLLATE utf8mb4_unicode_ci NOT NULL,
  `created` datetime NOT NULL,
  `expires` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_snippets_created` (`created`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```