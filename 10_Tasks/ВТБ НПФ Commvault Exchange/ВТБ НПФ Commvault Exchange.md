---
task: TASK1268343
customer: "[[ВТБ НПФ]]"
system: "[[Commvault]]"
tags:
  - type/incident
  - status/active
created: 2026-02-27
summary:
---
Наблюдается проблема с индексами:
```
Failure Reason: ERROR CODE [23:108]: ArchiveIndex failed on MediaAgent [lg-ma] - Index files are missing. Job could have earlier run on a different MediaAgent possibly due to a failover.  
Source: lg-ma, Process: archiveIndex (Error Lookup Site: http://kb.commvault.com/#!/?q=%2223:108%22)  
Associated Clients: lg-cs,lg-ma,exchdag13-p3,exchdag13-p4
```

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