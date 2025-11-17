---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
first-name:
last-name:
birthday:
related:
aliases:
tags:
  - "#type/person"
summary:
---

## Last Contact
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

## Log

```dataview
TASK
WHERE icontains(text, this.file.name)
AND !icontains(text, "#task")
GROUP BY file.name as filename
SORT rows.file.ctime DESC
```

## Tasks
```dataview
TASK
WHERE icontains(text, this.file.name)
AND (icontains(text, "#task") OR icontains(text, "question"))
AND !completed
GROUP BY file.name as filename
SORT filename DESC
```
