---
created: 2026-01-17
up:
  - "[[10 Software Development]]"
related:
  - "[[Web Development]]"
aliases:
tags:
  - "#type/project"
  - "#status/active"
summary:
---
## Фичи Jet Spares 1.0
- [x] Дашборд с возможность создания расчёт
- [ ] Страница всех конфигов
	- [ ] Поиск по TASK
	- [ ] Поиск по серийнику
	- [ ] Поиск по модели
	- [ ] Фильтр по типу (сервер, СХД)
	- [ ] Страница конфига
		- [ ] Возможность скачать конфигу в xls
		- [ ] Возможность скопировать конфиг к себе в заявку
- [ ] Страница всех компонент
	- [x] Фильтр по категориям
	- [x] Поиск по парт номеру
	- [x] Поиск по описанию
	- [ ] Редактирование компонента
	- [ ] Шаблон ТМЦ ?
	- [ ] Импорт из CSV
- [ ] Страница товарных категорий
	- [x] Фильтр по типу
	- [ ] Импорт категорий 
	- [ ] Импорт из CSV
- [ ] Конфигуратор
	- [x] Возможность добавить оборудование
	- [ ] Возможность отредактировать конфиг
	- [x] Возможность удалить конфиг
	- [ ] Возможность продублировать конфиг
	- [x] Таблица компонент
	- [x] Возможность добавить компонент
	- [x] Возможность удалить компонент
	- [x] Возможность изменить компонент
- [ ] Страница заявки
	- [ ] Возможность изменить поля (название, номер, тип)
	- [ ] Возможность изменить сроки расчёта
	- [ ] Возможность сменить текущий статус (черновик/опубликован)
	- [ ] Возможность удалить расчёт
- [ ] Страница ЗИП
	- [ ] Возможность скачать ЗИП в xls
	- [ ] Возможность изменить перезаписать посчитанное значение для каждого компонент
	- [ ] Возможность сменить текущий статус (черновик/опубликован)
- [ ] Калькуляция расчёта

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