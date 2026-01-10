---
uuid: 20230829120515
created: 2023-08-29T12:05:15
alias:
---

# [[Pacemaker]]

>[!note]
>Red Hat Enterprise Linux 7 and Red Hat Enterprise Linux 6 cluster nodes are not  
compatible. All nodes in a Pacemaker cluster must use the same major version of Red  
Hat Enterprise Linux; nodes running different major versions may not be mixed. 
Red Hat Enterprise Linux 7 clusters use Corosync 2.x for communication, while Red Hat Enterprise Linux 6 Pacemaker clusters use Corosync 1.x.

## Installation
The [[Cluster]] configuration software is provided by the [[pcs]] package. The pcs package requires the [[corosync]] and [[Pacemaker]] packages, which are automatically installed as dependencies if the installation is performed with [[yum]]. The fencing agents need to be  
installed on each of the cluster nodes. The fence-agents-all package pulls in all fencing agent packages that are available.
```bash
[root@nodeY ~]# yum install pcs fence-agents-all
```
### Configuring firewall
Cluster communication needs to be allowed by the firewall on all cluster nodes. The standard firewall service on a [[Red Hat Enterprise Linux]] 7 system is [[firewalld]]. The [[firewalld]] service comes with a standard service called `high-availability` to allow  
cluster communication.
```bash
[root@nodeY ~]# firewall-cmd --permanent --add-service=high-availability
[root@nodeY ~]# firewall-cmd --reload
```

### Enabling pcsd cluster configuration on the node
The [[pcsd]] service provides the cluster  configuration synchronization and the web front end for cluster configuration. The service is required  on all cluster nodes. The pcsd service needs to be enabled and started on all [[Cluster]] nodes with  [[systemctl]]
```bash
[root@nodeY ~]# systemctl enable pcsd  
[root@nodeY ~]# systemctl start pcsd
```
The system user `hacluster` is used by [[pcsd]] for cluster communication and configuration. It is  recommended to use the same password for the hacluster user among all nodes in the cluster.
```bash
[root@nodeY ~]# echo redhat | passwd --stdin hacluster
```
The [[pcsd]] service requires the cluster nodes to get authenticated with the user `hacluster` and the  password of this user on one of the cluster nodes:
```bash
pcs cluster auth \
192.168.0.201 \
192.168.0.202 \
192.168.0.203 \
-u hacluster -p redhat
```

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[High-availability]]