---
created: 2025-11-17 10:50
up:
  - "[[Work]]"
related: "[[Data Domain]]"
aliases:
  - TASK1155498
tags:
  - type/incident
  - status/archived
summary:
---
## Итог
IRH работает. Заказчик “удалял” данные из NetWorker командой nsrmm, данные удалялись из БД, но оставались на дисках.
Вернуть обратно получилось с помощью scanner.

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
