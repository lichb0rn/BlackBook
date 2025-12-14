---
up:
  - "[[Jet Spares]]"
related: 
created: 2025-06-01
in:
---
- Нужно добавить альтернативные номера в `SparesEstimate`
- ~~Убрать `DomainEvent` из `DeviceConfiguration`. Лучше сделать последовательный код, чем на ивентах. В будущем будет проще переносить `DeviceConfiguration` в `SparesCalculation`  агрегат~~.
- `CalculationService` пересчёт в двух случаях:
	- добавили `forecast period`
	- добавили/убрали конфиг или компонент