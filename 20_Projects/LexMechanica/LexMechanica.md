---
created: 2025-11-19 06:31
up:
  - "[[10 Software Development|Software Development]]"
related: "[[Work]]"
aliases:
  - Анализ логов
tags:
  - "#type/project"
  - "#status/active"
summary: Исправить баг парсинга
---
## Logs or Sprints
```dataview
TASK
WHERE icontains(text, this.file.name)
AND icontains(text, "#log/sprint")
GROUP BY file.name as filename
SORT filename DESC
```

## Sub Projects
```dataview
TABLE WITHOUT ID
	file.link as "Sub Project",
	created,
	summary,
	tags
FROM !"x/Templaes"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/project")
SORT filename DESC
```

## Meetings
```dataview
TABLE WITHOUT ID
	file.link as sessions,
	created,
	participants,
	summary
FROM !"x/Templates"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/meeting")
SORT filename DESC
```

## Related Notes
```dataview
TABLE WITHOUT ID
	file.link as session,
	created,
	summary
FROM !"x/Templates"
WHERE icontains(up, this.file.link)
AND !icontains(tags, "type/meeting")
OR icontains(related, this.file.link)
SORT filename DESC
```

## Tasks and Questions

### Open
```dataview
TASK
WHERE icontains(text, this.file.name)
AND (icontains(text, "#task") OR icontains(text, "question"))
AND !completed
GROUP BY file.name as filename
SORT filename DESC
```
### Closed
```dataview
TASK
WHERE icontains(text, this.file.name)
AND (icontains(text, "#task") OR icontains(text, "question"))
AND completed
GROUP BY file.name as filename
SORT filename DESC
```


## References  
- [[gRPC Microservice Structure in GO (DDD and Hexagonal Architecture)]]
- Для конфигов в `yaml`можно использовать https://github.com/goccy/go-yaml
- Примеры архитектуры на [[Golang]]: https://github.com/golang-school/evolution
- Пример организации файлов для [[NextJS]]: https://github.com/webdevcody/health-tracker/tree/main

## Status Tracking  
- **Active:** `#projects/active`  
- **Paused:** `#projects/paused`  
- **Finished:** `#projects/finished`  
- **Archived:** `#projects/archived`  