---
created: 2025-11-16 20:14
up:
  - "[[00 Maps]]"
related:
aliases:
  - Software Development
  - Programming
  - Coding
  - Программирование
  - Разработка ПО
tags:
  - type/moc
summary: Map of Content по разработке ПО
---

## Projects

### Active
```dataview
TABLE WITHOUT ID
	file.link as "Sub Project",
	created,
	summary,
	tags
FROM !"x/Templaes"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/project")
OR icontains(tags, "type/area")
AND icontains(tags, "status/active")
SORT filename DESC
```

### Finished
```dataview
TABLE WITHOUT ID
	file.link as "Sub Project",
	created,
	summary,
	tags
FROM !"x/Templaes"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/project")
OR icontains(tags, "type/area")
AND icontains(tags, "status/finished")
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
AND !icontains(tags, "#type/project")
SORT filename DESC
```

[[Distributed Computing]]