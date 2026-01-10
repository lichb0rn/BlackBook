---
status: in-progress
tags:
  - "#type/project"
links: "[[Projects]]"
deadline: 
area: "[[Development]]"
---
# Описание
Single-Page Application для подсчёта количества запасных частей к оборудованию.

# Архитектура
Используется [[Feature-Sliced Design]]


## Notes
- ~~duplicate - фича, можно перенести в /features~~
- можно проверить css `fit-content` для ячеек таблицы
- переосмыслить цвета: [[Color generator and resources]]
- ~~TemplateSection не отражает сути названия~~
- Можно добавить [[buildSelector]] и [[buildSlice]] 
- ~~Удаления срока можно сделать в виде тега, по наведению на который отображается курсор удаления~~
- ~~Нужно зарезервировать место для ошибки в FormRow, иначе прыгает~~
- перенести кнопку редактирования таска поближе к названию
- Для работы с [[IndexedDB]] можно подумать об использовании `useSyncExternalStore` [useSyncExternalStore – React](https://react.dev/reference/react/useSyncExternalStore)
- <mark style="background: #D2B3FFA6;">Обсудить с Максом, нужно ли отдельное поль альтернативных партов.</mark>
	- Может есть смысл схлопнуть в одно?
- ~~<mark style="background: #FFB86CA6;">ТЕСТИРОВАТЬ</mark>:~~
	- ~~После смены id парта на парт номер, могут быть проблемы с обновлением описания, при наличии парта в других конфига~~ 
	 - ~~Сменил парт. Сам парт-номер сменился, а id остался прежним~~ 
	 - Откатил. Не удобно менять, лучше сделать поиск в базе по парт номеру
- Форма добавления запчасти слишком длинная
	- Разбить на 2 колонки?
- Подсчет общего количества через reducer?
	- Отдельный слайс для `DeviceComponent`
- ❓Привязать id партийника к `partNumber` и сделать нередактируемым
- Перенести комментарий в `Component`
- Можно сделать `NavigationHeader` более универсальным на примере слота: [[TaskList]]
	- Выделяем item с props `actions: ReactNode`, а вместо ноды передаём фрагмент

# Bugs
- [x] Убрать кнопку "Добавить запчасть", если не выбран конфиг ✅ 2024-02-24
- [x] При сохранении таска, сохраняется вся схема, включает `isLoading`, `isError` ✅ [[2024-02-24]]
	- Убрал таск в data поле схемы


## Related Info
[[Headless Component a pattern for composing React UIs]]
![[Pasted image 20240213191458.png]]
