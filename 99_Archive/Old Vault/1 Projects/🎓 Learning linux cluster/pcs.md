---
uuid: 20230829152533
created: 2023-08-29T15:25:33
alias:
---

# [[pcs]]

Проверить статус кластера можно командой:
```shell
[root@node1 ~]# pcs cluster status
Cluster Status:
 Stack: corosync
 Current DC: node2.localdomain (version 1.1.23-1.el7_9.1-9acf116022) - partition with quorum
 Last updated: Tue Aug 29 15:28:41 2023
 Last change: Tue Aug 29 15:27:39 2023 by hacluster via crmd on node2.localdomain
 3 nodes configured
 0 resource instances configured

PCSD Status:
  node1.localdomain (192.168.0.201): Online
  node2.localdomain (192.168.0.202): Online
  node3.localdomain (192.168.0.203): Online
```

### Prohibiting a cluster node from hosting resources
When a node is put in `standby` mode, it does not get any resources assigned. Resources that are currently running on the node are migrated to another node.

The `pcs cluster standby` command can put the local node in standby mode.
```shell
[root@node1 ~]# pcs cluster standby node3.localdomain
[root@node1 ~]# pcs status
Cluster name: linuxdemo

WARNINGS:
No stonith devices and stonith-enabled is not false
Corosync and pacemaker node names do not match (IPs used in setup?)

Stack: corosync
Current DC: node1.localdomain (version 1.1.23-1.el7_9.1-9acf116022) - partition with quorum
Last updated: Wed Aug 30 15:19:47 2023
Last change: Wed Aug 30 15:19:29 2023 by root via cibadmin on node1.localdomain

3 nodes configured
0 resource instances configured

Node node3.localdomain: standby
Online: [ node1.localdomain node2.localdomain ]
```

The resource constraint that has been applied by putting a node in standby can be removed with `pcs cluster unstandby`.
```shell
[root@node1 ~]# pcs cluster unstandby node3.localdomain
```

Removing the resource constraint **does not necessarily mean that a resource that was  previously running on a node before it was put in standby mode migrates back**.


---

## 📇 Additional Metadata
- 🛠️ Status::  #🌱 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[High-availability]]