---
task: TASK1249061
customer: "[[Арована Капитал]]"
system: "[[Commvault]]"
tags:
  - type/incident
  - status/active
created: 2026-02-04
summary:
---
> Суть вопроса в следующем: антивирус обнаружил на сервере CommVault потенциально вредоносный файл по следующему пути: K:\AMSK01NN09_13\V5SY3R_04.22.2022_14.59\CV_MAGNETIC\V_7318541\CHUNK_127189059\SFILE_CONTAINER_006//14 Akagi64.exe
> K:\AMSK01NN09_13 - это Mount Path для Magnetic Library, которая используется в нескольких копиях с включенной Global Deduplication.
> Вопрос: как найти все бекапные задания, которые используют данный блок ?
> 
> Попробовал из БД CommServe получить такую информацию по chunk id, и сначала это удалось (возвращал jobid), но сейчас уже нет - видимо, та копия уже проэкспайрилась. Но файл на диске всё ещё существует, поэтому подозреваю, что он используется другими копиями.


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