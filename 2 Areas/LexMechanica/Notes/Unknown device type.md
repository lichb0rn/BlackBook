---
up:
  - "[[LexMechanica]]"
related: 
created: 2025-05-25
---
Исправить `device type`, который приходи в `ParseJob`:
```sh
listener-1  | time=2025-05-25T14:55:04.117Z level=ERROR source=/app/internal/ports/ports/rabbitmq/consumer.go:139 msg="Failed to unmarshal message" error="unknown device type: vnx2" delivery_tag=1
listener-1  | time=2025-05-25T14:55:04.117Z level=ERROR source=/app/internal/ports/ports/rabbitmq/consumer.go:173 msg="Rejecting message" requeue=false delivery_tag=1

listener-1  | time=2025-05-25T14:56:01.617Z level=ERROR source=/app/internal/ports/ports/rabbitmq/consumer.go:139 msg="Failed to unmarshal message" error="unknown device type: vnxe" delivery_tag=2
```