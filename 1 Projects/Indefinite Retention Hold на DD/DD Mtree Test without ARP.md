---
created: 2025-11-18 10:55
up:
  - "[[Indefinite Retention Hold на DD]]"
related: "[[Data Domain]]"
aliases:
  - mtree без automatic-retention-period
tags:
  - type/note
summary:
---
1. Сделал mtree без automatic retention period:
```sh
sysadmin@ddve# mtree retention-lock status mtree /data/col1/irhtest
Option                                      Value                                       
-----------------------------------------   --------------------------------------------
Retention-lock                              enabled                                     
Retention-lock mode                         governance                                  
Retention-lock uuid                         21cb4d8c6ce2f3d1:5830bae7595a14d3           
Retention-lock min-retention-period         720minutes                                  
Retention-lock max-retention-period         7days                                       
Retention-lock automatic-retention-period   not set                                     
Retention-lock automatic-lock-delay         5minutes                                    
Retention-lock indefinite-retention-hold    enabled (since Wed Nov 19 11:21:35 MSK 2025)
-----------------------------------------   --------------------------------------------
```

2. Создал файлы:
```sh
-rw-rw-r--  1 nobody   nogroup    24 Nov 17 12:21 test.txt
-rw-rw-r--  1 lichb0rn lichb0rn    0 Nov 19 11:00 test1.txt
-rw-rw-r--  1 lichb0rn lichb0rn    0 Nov 19 11:00 test2.txt
-rw-rw-r--  1 lichb0rn lichb0rn    0 Nov 19 11:03 test3.txt
```

3. report
```sh
Report for mtree: /data/col1/irhtest
File Path        Mode        Size(Bytes)        Expiration Date
/data/col1/irhtest/test1.txt governance 1024 Wed Nov 19 23:30:00 2025
/data/col1/irhtest/test2.txt governance 1024 Wed Nov 19 23:30:00 2025
/data/col1/irhtest/test3.txt governance 1024 Wed Nov 19 23:30:00 2025
Total files: 3

** MTree /data/col1/irhtest is under indefinite retention hold (since Wed Nov 19 11:21:35 MSK 2025)
```

4. Проверяем возможность удаления после окончания retention периода:
```sh
➜  ddtest1 rm test3.txt 
rm: удалить защищённый от записи пустой обычный файл 'test3.txt'? y
rm: невозможно удалить 'test3.txt': Отказано в доступе
```

## Вывод