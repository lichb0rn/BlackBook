---
created: 2026-02-19
tags:
  - type/note
source:
related:
area: "[[Work]]"
up:
  - "[[EMC VMax]]"
---
Залогиниться на SP под пользователем admin (пароль по умолчанию EMC2Admin), домен localhost

Зайти в O:\utilo, создать каталог frd (если его еще нет)
запустить sp_backup_restore.exe, нажать галку Enable Backup, затем кнопку Backup,
выбрать Bootstrap Backup.


regedit /e o:\macname1.reg HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
regedit /e o:\macname2.reg HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\ComputerName
regedit /e o:\Serialtmp.reg HKEY_LOCAL_MACHINE\SOFTWARE\EMC\SiteInfo


Забрать 4 полученных файла:
O:\utilo\backup\Bootstrap_Backup_SN...
o:\macname1.reg
o:\macname2.reg
o:\Serialtmp.reg