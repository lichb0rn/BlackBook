---
task:
customer:
system:
tags:
  - type/incident
  - status/active
created: <% tp.date.now("YYYY-MM-DD") %>
summary:
---
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