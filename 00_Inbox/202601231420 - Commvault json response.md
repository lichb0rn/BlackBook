---
created: 2026-01-23
tags:
  - type/note
source:
related:
area:
up:
  - "[[Выгрузка клиентов через api - кластеры и их ноды]]"
---
## Instance
Для кластера Postgres есть ноды:
```json
// /instance?clientId=
{
	"instanceProperties": [
		{
			"postGreSQLInstance": {
				"nodes": [
		          {
		            "clusterPriority": 0,
		            "physicalClient": {
		              "clientId": 1023,
		              "clientName": "astra-pg-2",
		              "displayName": "astra-pg-2"
		            },
		          }
		        ],
			}
		}
	]
}
```

Для файлового кластера Win - нет.

## Client properties
```json
"ActivePhysicalNode": {
  "hostName": "10.31.181.42",
  "clientId": 1005,
  "clientName": "SQL"
}
```