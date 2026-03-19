---
tags:
  - type/insight
source: https://discuss.kubernetes.io/t/the-connection-to-the-server-localhost-8080-was-refused-did-you-specify-the-right-host-or-port/1464
related:
  - "[[Контейнерная платформа Штурвал]]"
area:
up:
  - "[[MOC - Kubernetes]]"
---
Для работы [[kubectl]] с кластером [[MOC - Kubernetes]] (например, при взаимодействии с [[Контейнерная платформа Штурвал]]) нужно скопировать `admin.conf`:
 
```sh
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

