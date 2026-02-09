---
task: TASK1239203
customer: "[[ИЛИМ]]"
system: "[[Vplex]]"
tags:
  - type/incident
  - status/archived
  - log
created: 2026-01-28
summary: Обновление завершено
---
# Summary
- Влад Лосев не смог скачать микрокод, т.к. нет доступа. Пришлось ставить 6.2.1.0.0.519
- В процессе получил ошибки:
	- `Verify RecoverPoint cluster registrations.. ERROR`
	- Ошибка VPLEX-54511
	- Исправил `emc-internal ndu start --skip-recoverpoint-cluster-registration-check`
- Ошибки Witness  при генерации сертификата:
	- `Error during Cluster Witness Server Host Certificate configuration: CWS Permission denied`
	- Ошибка VPLEX-54198
	- Исправил настройкой NTP на обоих vplex и Witness

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