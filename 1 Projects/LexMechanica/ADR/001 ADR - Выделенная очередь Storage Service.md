---
tags:
  - "#adr/accepted"
created: 2025-06-29
project: "[[LexMechanica]]"
---
## Context
Сейчас используется один [[RabbitMQ]] топик для всего. В итоге все сервисы имеют доступ ко всем данным. Также топики плохо масштабируются. Когда gateway/frontend отправляет событие `created`, [[LM-Triage]] сразу его подхватывает и тоже шлёт событие `accepted`. В итоге возникает [[Race Condition]] в Storage Service, и создаются 2 одинаковые записи в БД.

## Decision
Решение - переделать работы с очередями. Gateway/Frontend шлёт в отдельную очередь событие о загрузке логов. Эту очередь слушает только Storage Service. После записи в БД, он отправляет сообщение `created` в топик. В итоге миркосервис может ответить сообщением `accepted`, чей статус будет корректно отображён.

## Consequences


---
## Status Tracking  
- **Proposed:** `#adr/proposed`  
- **Accepted:** `#adr/accepted`  
- **Rejected:** `#adr/rejected`  
- **Replaced:** `#adr/superseded`  