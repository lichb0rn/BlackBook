---
created: 2026-03-16
tags:
  - type/note
source:
related:
area:
up:
aliases:
  - Command Query Responsibility Segregation
  - CQRS
---
# How to implement basic CQRS

CQRS подразумевает: вместо одной большой модели данных, используемой для чтения и записи, мы используем две.
Одна модель для чтения и одна для записи. CQRS также подразумевает, что у нас есть два пути: запрос (query) и команда (command).

> [!Quote] [[Go with Domain]]
> CQRS (Command Query Responsibility Segregation) was initially described by Greg Young. It has one simple assumption: instead of having one big model for reads and writes, you should have two separate models. One for writes and one for reads. It also introduces concepts of command and query, and leads to splitting application services into two separate types: command and query handlers.

![[POST API.png]]


## CQRS Documents by Greg Young

![[cqrs_documents.pdf]]