---
created: 2026-01-13
tags:
  - type/note
source: "[[Let's Go Further]]"
related:
area: "[[10 Software Development]]"
project: "[[Greenlight]]"
---
# Makefile

## Phony targets
`target` из makefile могут пересекаться с именем файла. Например:
```Makefile
run/api:
	go run ./cmd/api
```
Если существует такой файл, то таргет выпадет в ошибку:
```sh
$ mkdir run && touch run/api
$ make run/api
make: 'run/api' is up to date.
```
Для таргетов, которые выполняют роль правил, существуют phony targets:
```Makefile
.PHONY: target
target: prerequisite-target-1 prerequisite-target-2 ...
	command
	command
```

## Links and context

## References

