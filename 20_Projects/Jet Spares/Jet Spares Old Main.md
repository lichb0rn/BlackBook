
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
AND icontains(tags, "project/note")
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


## Notes & Progress  
- Можно использовать `Set` для `DeviceComponent`, `ForecastPeriod`.
- [[Traefik]] вместо [[NGINX]]
- `filter` в ComponentsQuery раньше использовался для фильтрации по категориям
	- <font color="#d83931">Исправить на фронте</font>
- Проверять, если таск с таким номером у пользователя, при создании нового расчёта
- Если кто-то оверрайтит посчитанное количество до 0, то удалять из Calculation
- [[JS Refactoring]]


## Links & References  
- [[Add Authentication to MongoDB]]
- [[CUSTOM MONGODB MIGRATION]]
- [[How I Design Beautiful SaaS (Frontend & UI Guide)]]
- [[JS Deployment]]

## Status Tracking  
- **Active:** `#projects/active`  
- **Paused:** `#projects/paused`  
- **Finished:** `#projects/finished`  
- **Archived:** `#projects/archived`  