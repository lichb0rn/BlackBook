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
## Ноды
- worker node
- master node
![[Pasted image 20260209161623.png]]

## Components
- API Server
	- фронтенд для k8s
	- принимает команды
- [[etcd]]
	- распределенный key/value store
- kubelet
	- агент, запущенный на каждой ноде в кластере
- scheduler
	- отвечает за распределение работы между нодами
- controller
	- следит за нодами, поднимает, если что-то упало
- container runtime
	- docker и другие

