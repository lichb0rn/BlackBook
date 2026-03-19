---
tags:
  - type/note
source:
related:
area:
up:
---
Для работы [[kubectl]] с кластером [[MOC - Kubernetes]] (например, при взаимодействии с [[Контейнерная платформа Штурвал]]) нужно скопировать
 
```sh
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

