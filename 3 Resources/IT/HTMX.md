---
up:
  - "[[Web Development]]"
related: "[[HTMX + Go Build Fullstack Applications]]"
created: 2025-05-31
---
По умолчанию, AJAX запросы уходят по `“natural” event of an element`. Т.е.:
- `input`, `textarea` & `select` are triggered on the `change` event
- `form` is triggered on the `submit` event
- everything else is triggered by the `click` event

Чтобы изменить, можно воспользоваться `hx-trigger`.