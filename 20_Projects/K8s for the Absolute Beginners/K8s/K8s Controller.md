---
created: 2026-02-16
tags:
  - type/note
source:
related:
area:
up:
  - "[[Kubernetes]]"
---
- Следит за состоянием [[pods]]
- Осуществляет load balancing & scaling
![[Pasted image 20260216170956.png]]

- replication controller был заменен на replica set

# ReplicationController
## Создание replication controller

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: frontend
spec:
  template:
	metadata:
	  name: nginx-2
	  labels:
	    app: myapp
	    type: frontend
	spec:
	  containers:
	    - name: nginx
	      image: nginx
  
  replicas: 3
```

Запуск `kubectl create -f rc-definition.yaml`

## Статус

```sh
kubectl get replicationcontroller
```


# ReplicaSet
## Создание

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: frontend
spec:
  template:
	metadata:
	  name: nginx-2
	  labels:
	    app: myapp
	    type: frontend
	spec:
	  containers:
	    - name: nginx
	      image: nginx
  
  replicas: 3
  selector: 
	matchLabels:
	  type: frontend
```

Запуск `kubectl create -f rs-definitiona.yaml`

## Статус

```sh
kubectl get replicaset
```

## Labels & Selectors

![[Pasted image 20260216172638.png]]

## Scale

- Исправить `replicas` в файле и выполнить:
```sh
kubectl replace -f replicaset.yaml
```

- Обновить из cli:
```sh
kubectl scale --replicas=6 -f replicaset.yaml
```

```sh
kubectl scale --replicas=6 replicaset myapp-replicaset
```