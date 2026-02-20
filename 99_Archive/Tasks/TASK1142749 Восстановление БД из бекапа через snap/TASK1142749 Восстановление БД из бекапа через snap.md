---
created: 2025-11-14
up:
related: "[[Commvault]]"
aliases:
  - TASK1142749
tags:
  - type/incident
  - status/archived
summary: Вендор подтвердил принципиальную невозможность block level backup
task: TASK1142749
---
## Итог
RedOS заказчика не поддерживается cvbf драйвером Commvault. Для работы Driverless режима нужно настраивать аппаратные снапшоты.

/usr/lib/postgresql/15/bin/pg_ctl -D /data/pgdata -l logfile start
waiting for server to start.... done
server started
postgres@astra-pg-2:~$ 


Собрал ядро по инструкции [[Пошаговое руководство как собрать ядро Linux с нуля]] с `CONFIG_MODULE_FORCE_LOAD=y`
После чего через `modprobe -f` попытался загрузить модуль:
```sh
/opt/commvault/CVBLK# insmod -f cvbf-6.1.90-1-generic.ko 
insmod: ERROR: could not insert module cvbf-6.1.90-1-generic.ko: Unknown symbol in module
```

Вывод dmesg:
```sh
[ 1587.298116] cvbf: Unknown symbol kmem_cache_alloc_trace (err -2)
[ 1587.298124] cvbf: Unknown symbol __fentry__ (err -2)
[ 1587.298143] cvbf: Unknown symbol printk (err -2)
[ 1587.298149] cvbf: Unknown symbol PDE_DATA (err -2)
[ 1587.298156] cvbf: Unknown symbol bio_advance (err -2)
[ 1587.298177] cvbf: Unknown symbol blk_cleanup_disk (err -2)
[ 1587.298192] cvbf: Unknown symbol complete_and_exit (err -2)
```

## Evidence
[[2025-12-09 TASK1142749 Результат тестового прогона FSBased бэкапа]]


## Logs or Sprints
```dataview
TASK
WHERE icontains(text, this.file.name)
AND icontains(text, "#log/sprint")
GROUP BY file.name as filename
SORT filename DESC
```

## Sub Projects
```dataview
TABLE WITHOUT ID
	file.link as "Sub Project",
	created,
	summary,
	tags
FROM !"x/Templaes"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/project")
SORT filename DESC
```

## Meetings
```dataview
TABLE WITHOUT ID
	file.link as sessions,
	created,
	participants,
	summary
FROM !"x/Templates"
WHERE icontains(up, this.file.link)
AND icontains(tags, "type/meeting")
SORT filename DESC
```

## Related Notes
```dataview
TABLE WITHOUT ID
	file.link as session,
	created,
	summary
FROM !"x/Templates"
WHERE icontains(up, this.file.link)
AND !icontains(tags, "type/meeting")
OR icontains(related, this.file.link)
SORT filename DESC
```

## Tasks and Questions

### Open
```dataview
TASK
WHERE icontains(text, this.file.name)
AND (icontains(text, "#task") OR icontains(text, "question"))
AND !completed
GROUP BY file.name as filename
SORT filename DESC
```
### Closed
```dataview
TASK
WHERE icontains(text, this.file.name)
AND (icontains(text, "#task") OR icontains(text, "question"))
AND completed
GROUP BY file.name as filename
SORT filename DESC
```
