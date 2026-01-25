---
created: 2026-01-24
up:
  - "[[10 Software Development|Software Development]]"
related:
  - "[[Work]]"
  - "[[Golang|Go]]"
  - "[[NextJS]]"
aliases:
  - Анализ логов
tags:
  - "#type/project"
  - "#status/active"
summary: Продолжить работу над парсером brocade
---
Тестовая заявка: [TASK0913767](https://sd.jet.su/record/itsm_infosys_task/174437466804378123)

## Logs
```dataview
TASK
WHERE icontains(text, this.file.name)
AND icontains(text, "#type/log")
GROUP BY file.name as filename
SORT filename DESC
```

## Work Sessions
![[Project.base#Work Sessions / Meetings]]

## Child Notes
![[Project.base#Child Notes]]

## Related Notes
![[Project.base#Related Notes]]


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