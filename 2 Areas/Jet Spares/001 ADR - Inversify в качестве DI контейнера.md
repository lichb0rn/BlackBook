---
tags:
  - "#adr/accepted"
created: 2025-05-03
project: "[[Jet Spares]]"
---
## Context
В проекте уже довольно много объектов. Почти все создаются бесконтрольно через barrel-файл `index.ts`. Из-за этого стало сложно добавлять unit-тесты в проект.

## Decision
Для решение проблемы было решено добавить [[Inversify]] в качестве [[Dependency Injection|DI]]-контейнера.

## Consequences


---
## Status Tracking  
- **Proposed:** `#adr/proposed`  
- **Accepted:** `#adr/accepted`  
- **Rejected:** `#adr/rejected`  
- **Replaced:** `#adr/superseded`  