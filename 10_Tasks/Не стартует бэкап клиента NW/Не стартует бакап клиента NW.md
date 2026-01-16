---
task: TASK1223598
customer: "[[Тандер]]"
system: "[[NetWorker]]"
tags:
  - type/incident
created: 2026-01-15
summary: Проблема на стороне ОС, не работает VSS
---

>[!quote]
>После старта задания файлового бакапа на клиенте оно зависает.

>[!quote]
>На клиенте trassirgk4-2 скрипт nsrget зависает на строке сбора информации collecting extended host information. Поэтому в архиве папка с тем, что скрипт сумел собрать. Переустановка клиента не помогла. Подключение с консоли и modify client wizard выполняется успешно. 
>Выполнил задание с режимом дебага 9: nsrworkflow -D9 -p unscheduled -w Once_Workflow, ждал 10 мин, далее прервал, лог загрузил. Также загружен daemon.raw с рендером за последние сутки.

>[!quote]
>Также у нас есть клиент trassirgka-2 и на нем происходит сбой бакапа. Ошибка указана ниже. Не помогла ни перезагрузка клиентской машины, ни переустановка клиента. Подключение с консоли и modify client wizard выполняется успешно. Выполнил задание с режимом дебага 9: nsrworkflow -D9 -p unscheduled -w Once_Workflow, лог загрузил. Также загружен daemon.raw с рендером за последние сутки. Ссылка для скачивания указана выше.
>_VSS OTHER: ERROR: VSS failed to process snapshot: Unable to create the VSS snapshot._
_197048:save: Unable to save the SYSTEM STATE save sets and create the snapshot: Unable to create the VSS snapshot._
_176571:save: Step (4 of 5) for PID-11352: Unable to complete the backup of the disaster recovery save sets. See the savegrp log to track the closure steps of the backup._
_176572:save: Error occurred during the backup of the disaster recovery save sets._
_--- Job Indications ---_
_trassirgka-2.corp.tander.ru:pseudo_saveset: retried 1 times._


# Logs
[[202601151656 - Логи Тандер для trassirgka-2]]
- Проверить https://tools.jet.su/emc_kb/000224041/





