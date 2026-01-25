---
task: TASK1232198
customer: "[[Сбербанк Страхование]]"
system: "[[Commvault]]"
tags:
  - type/incident
  - status/active
created: 2026-01-23
summary:
---

> [!NOTE]
> У нас есть задача получить занимаемый объём бэкапов каждого клиента. Мы выполнили это через отчёт Chargeback Details и поля Total Data Written.
> Однако мы столкнулись с проблемой псевдо-клиентов: кластеров БД и ФС. Из отчёта мы можем взять размер БД с кластера и, например, прибавить его к 1ой ноде кластера по умолчанию. Но для этого нам нужно чётко понимать какая сущность является кластером и какие в него входят ноды (именно физические сервера или реальные ВМ на которых установлен агент).
> 
> Как из массива всех заведённых в комволте клиентов через api вытащить список кластеров с их узлами?
> 
> Через запрос вида ниже мы смогли получить поле «ClusterMembers», но там сам кластер и ноды указаны перекрёстно друг на друга, а для файлового кластера всё совсем не наглядно
> 

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