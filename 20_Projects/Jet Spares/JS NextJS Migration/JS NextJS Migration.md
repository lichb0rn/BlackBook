---
created: 2025-11-16 20:07
up:
  - "[[Jet Spares]]"
related:
aliases:
tags:
  - "#type/project"
  - "#status/active"
summary: Доделать action по добавлению в конфиг компонента
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
AND icontains(tags, "type/note")
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
