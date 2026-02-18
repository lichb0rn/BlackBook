---
task: TASK1220136
customer: "[[ИЛИМ]]"
system: "[[PowerVault ME5]]"
tags:
  - type/incident
  - status/archived
created: 2026-01-19
summary: Определить причину не удалось
---
## Результат
В рамках заявки не удалось определить точную причину возникновения проблемы.
Со стороны массива всё в норме, в SAN ошибок нет.
В случае повторения ситуации рекомендуется открыть заявку в момент появления. 
Снять supportsave/tech-support с коммутаторов, а с массива выполнить команды:

show controller-statistics
show disk-group-statistics

Если проблема появилась в пределах нескольких часов:
query metrics count all system.read-avg-response-time 

Дальше уже только так:
query metrics database historical time-range "start 2026-02-10 10:00 AM end 2026-02-10 11:00 PM" system.read-avg-response-time

## Описание
>[!quote]
>01 января в 6:48 и 07 января в 7:04 кратковременно пропадал LUN. Посмотрите со стороны массива, были ли какие-то проблемы.

>[!warning]
>Cluster Shared Volume is no longer accessible from this cluster node because of error '(1460)'.

Тома
- P1_L1_cl3-data2


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