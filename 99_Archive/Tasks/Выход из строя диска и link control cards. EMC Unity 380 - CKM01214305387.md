---
task: TASK1292721
customer: "[[MOC - ИЛИМ]]"
system: "[[EMC Unity]]"
tags:
  - type/incident
  - status/archived
created: 2026-03-10
summary:
---
[[2026-03-18]]
- Отправили новый диск
- Major Express 2000443016, 005053152, Cерийный номер S400N9BL


Старый диск
Part Number 005053153, Serial Number X110A01FFQHG

Новый диск
Major Express 1999014887
Артикул 005053364,  Серийный номер 06G516KZ (DOA)

## Logs
```dataview
TASK
WHERE icontains(text, this.file.name)
AND icontains(text, "#type/log")
GROUP BY file.name as filename
SORT filename DESC
```


## Sub Tasks
![[Task.base#Sub Tasks]]

## Work Sessions
![[Task.base#Work Sessions / Meetings]]

## Child Notes
![[Task.base#Child Notes]]

## Related Notes
![[Task.base#Related Notes]]


## Tasks
```tasks
not done
description includes {{query.file.filenameWithoutExtension}}
sort by due
group by function task.file.filenameWithoutExtension
short mode
```

## Status Tracking  
- **Active:** `#status/active`  
- **Paused:** `#status/paused`  
- **Finished:** `#status/finished`  
- **Archived:** `#status/archived`  