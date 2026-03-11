---
created: 2026-02-09
tags:
  - type/note
source:
related:
area:
up:
  - "[[Kubernetes]]"
---
pod - "обёртка" над контейнером.
- обычно имеют 1-к-1 отношения с контейнерами
- можно иметь несколько контейнеров в одном pod
	- остальные контейнеры служат поддержкой для продуктивного приложения
![[Pasted image 20260209165020.png|700]]

## Deploy
```sh
kubectl run nginx --image nginx
kubectl get pods
```


