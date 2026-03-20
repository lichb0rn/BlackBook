---
task: TASK1299137
customer: "[[MOC - ИЛИМ]]"
system: "[[EMC XtremIO]]"
tags:
  - type/incident
  - status/active
created: 2026-03-13
summary: Перезагрузить контроллеры
---
## Notes
Нужно ребутнуть оба контроллера:
```sh
show-storage-controllers cluster-id=3

deactivate-storage-controller cluster-id=3 sc-id=2
ipmitool chassis power cycle

activate-storage-controller cluster-id=3 sc-id=2
```

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