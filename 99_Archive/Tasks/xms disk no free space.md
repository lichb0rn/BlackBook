---
task: TASK1293342
customer: "[[ИЛИМ]]"
system: "[[EMC XtremIO]]"
tags:
  - type/incident
  - status/archived
created: 2026-03-10
summary:
---
На xms кончилось место.
Решил вопрос скриптом:
```sh
run-script script="xms_disk_cleanup-v1.3-s4.0.0.py"
```

https://tools.jet.su/emc_kb/000012182/index.html
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