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
```sh
sysadmin@ddve# mtree retention-lock status mtree /data/col1/rlcetest
Option                                      Value                                       
-----------------------------------------   --------------------------------------------
Retention-lock                              enabled                                     
Retention-lock mode                         governance                                  
Retention-lock uuid                         4981551156fd5ecc:9f645b4d78c2d336           
Retention-lock min-retention-period         720minutes                                  
Retention-lock max-retention-period         1827days                                    
Retention-lock automatic-retention-period   not set                                     
Retention-lock automatic-lock-delay         120minutes                                  
Retention-lock indefinite-retention-hold    enabled (since Tue Nov 18 10:49:23 MSK 2025)
-----------------------------------------   --------------------------------------------

Report for mtree: /data/col1/rlcetest
File Path        Mode        Size(Bytes)        Expiration Date
/data/col1/rlcetest/test1.txt governance 1024 Wed Nov 19 10:00:00 2025
Total files: 1

** MTree /data/col1/rlcetest is under indefinite retention hold (since Tue Nov 18 10:49:23 MSK 2025)
```

