---
up:
  - "[[10 Software Development]]"
related:
  - "[[Golang]]"
aliases:
tags:
  - "#type/project"
  - status/paused
created: 2026-01-16
Next Action: Закончить проект
---
Создание интерпретатор на языке [[Golang]] по книге [[Writing an Interpreter in Go]]
Source code: https://interpreterbook.com/waiig_code_1.3.zip

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