---
task: TASK1269744
customer: "[[ИЛИМ]]"
system: "[[EMC VNX]]"
tags:
  - type/incident
  - status/active
created: 2026-02-27
summary: Заменить память и батарею
---
## Батарея
**Новая** 078-000-092-07, Серийный номер ACPF2132500225
Старая 

## Память
Новая 100-563-382, Серийный номер 802C0F15060EB148FB
Старая

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