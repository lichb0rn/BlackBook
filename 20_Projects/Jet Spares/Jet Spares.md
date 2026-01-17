---
created: 2026-01-17
up:
  - "[[10 Software Development]]"
  - "[[**Area of Parent Project**]]"
related:
  - "[[Web Development]]"
aliases:
tags:
  - "#type/project"
  - "#status/active"
summary:
---
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