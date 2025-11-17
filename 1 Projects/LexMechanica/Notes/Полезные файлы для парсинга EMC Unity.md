---
up:
  - "[[LexMechanica]]"
related: "[[EMC]]"
created: 2025-05-10
in:
---
`Unity/spa/cmd_outputs/svc_data/svc_diag.txt`

`Unity/spa/cmd_outputs/smcli.txt`

`Unity/spa/cmd_outputs/sptool_-s_ALL.txt`

`Unity/spa/cmd_outputs/uptime.txt`

`Unity/spa/cmd_outputs/df_-Th.txt`

Но лучше парсить `*.sef` файлы

В `*.sef` файлах разные данные.
Например, в файле `spa.sef`:
```
enclosure_power[0.0.0].model=12V P/S WITH 12VSTBY AND FAN    
enclosure_power[0.0.0].ps_0_fault=0
enclosure_power[0.0.0].ps_0_powershutdown=0
```

А в `spb.sef`:
```
enclosure_power[0.0.0].needs_replacing=0
```

Нет модели и отметки `ps_fault`.