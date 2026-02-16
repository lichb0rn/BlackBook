---
task: TASK1258185
customer: "[[Пихта Банк]]"
system: "[[Commvault]]"
tags:
  - type/incident
  - status/paused
created: 2026-02-16
summary: Договорились отложить до марта проведение работ по настройке
---
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