---
created: 2026-03-16
tags:
  - type/source
source:
related:
area:
up:
  - "[[Контейнерная платформа Штурвал]]"
---

| Компонент  | Запись                                     | Комментарий                                                           |
| ---------- | ------------------------------------------ | --------------------------------------------------------------------- |
| API-server | api.<shturval_cluster_name>.<base_domain>. | А-запись для программного интерфейса приложений кластера управления   |
| Ingress    | *.<shturval_cluster_name>.<base_domain>.   | Wildcard-запись для доступа к прикладным функциям кластера управления |
| API-server | api.<client_cluster_name>.<base_domain>.   | А-запись для программного интерфейса приложений клиентского кластера  |
| Ingress    | *.<client_cluster_name>.<base_domain>.     | Wildcard-запись для доступа к приложениям клиентского кластера        |
|            |                                            |                                                                       |

– `<base_domain>` - DNS-зона организации
– `<shturval_cluster_name>` - имя кластера управления
– `<client_cluster_name>` - имя клиентского кластера