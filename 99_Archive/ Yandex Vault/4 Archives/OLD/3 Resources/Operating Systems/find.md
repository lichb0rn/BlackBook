---
aliases: ["find"]
---
MOC:  [[100 General IT]]

---

# Поиск
`$ find /etc -name passwd` - поиск файлов с именем `passwd` в каталоге `/etc`

`$ find /usr/share/ -size +10M` - поиск файлов более 10МБ
`$ find /mostlybig -size -1M `  - поиск файлов менее 1МБ
`$ find /bigdata -size +500M -size -5G -exec du -sh {} \;` - поиск файлов от 500Мб до 5Гб.

 
## Поиск по файлам конкретных пользователей
`$ find /home -user chris -ls`
`# find /home \( -user chris -or -user joe \) -ls`
`# find /etc -group ntp -ls`
`# find /var/spool -not -user root -ls`

## Поиск по правам доступа
`$ find /usr/bin -perm 755 -ls  
`788884 28 ­rwxr­xr­x 1 root root 28176 Mar 10 2014 /bin/echo`

`$ find /home/chris/ -perm -222 -type d -ls  
`144503 4 drwxrwxrwx 8 chris chris 4096 Jun 23 2014 /home/chris/OPENDIR`

## Поиск по дате и времени
`$ find /etc/ -mmin -10`

## Поиск с помощью `not` и `or` 
`$ find /var/allusers \( -user joe -o -user chris \) -ls`
`$ find /var/allusers/ -user joe -not -group joe -ls`