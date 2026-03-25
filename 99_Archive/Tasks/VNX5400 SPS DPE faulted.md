---
task: TASK1269744
customer: "[[MOC - ИЛИМ]]"
system: "[[EMC VNX]]"
tags:
  - type/incident
  - status/archived
created: 2026-02-27
summary: Заменить память и батарею
---
- [x] #task Вернуть запчасти TASK1269744 EMC VNX 5400, CKM00144602394 BBU + mem DIMM #7 DIMM_ECC Rank1 - SP A [[VNX5400 SPS DPE faulted]] ✅ 2026-03-12

## Батарея
**Новая** 078-000-092-07, Серийный номер ACPF2132500225
Старая 078-000-092-07, ACPF2142300003

## Память
Новая 100-563-382, Серийный номер 802C0F15060EB148FB
Старая 100-563-382, SN:802C0F14380D445D9F

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