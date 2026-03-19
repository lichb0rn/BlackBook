---
tags:
  - type/note
source:
related:
area:
up:
---
В рамках курса [[Администрирование Штурвал]] я неправильно настроил Network Policy Cilium.
В итоге пропал доступ к UI Штурвал.
Восстановил так:

```sh
user@master41:~$ kubectl get ciliumnetworkpolicies -A
No resources found
user@master41:~$ kubectl get ccnp
NAME        VALID
apache-np   True
user@master41:~$ kubectl delete ccnp apache-np
ciliumclusterwidenetworkpolicy.cilium.io "apache-np" deleted
```

>[!Warning]
>Предварительно нужно настроить работу [[kubectl]] по этой инструкции [[Настройка kubectl для работы с кластером]]

