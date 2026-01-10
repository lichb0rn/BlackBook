---
uuid: 20230908115206
created: 2023-09-08T11:52:06
alias:
---

# [[corosync]]

Конфиг: `/etc/corosync/corosync.conf`

По умолчанию настройки [[Quorum|кворума]]:
```shell
quorum {  
	provider: corosync_votequorum  
}
```

>[!note]
>Before making manual adjustments to the` /etc/corosync/corosync.conf` configuration file, it is advisable to schedule a maintenance window and shut down the cluster with `pcs cluster stop --all`.  This avoids unplanned cluster downtime, for example, due to configuration files that cannot be  parsed.

To enable the `last_man_standing` , `wait_for_all` , and `auto_tie_breaker` options, change the quorum directive in the `/etc/corosync/corosync.conf` file to include the options as follows:
```shell
quorum {  
	provider: corosync_votequorum  
	last_man_standing: 1  
	wait_for_all: 1  
	auto_tie_breaker: 1  
	auto_tie_breaker_node: lowest  
}
```
The content of the `corosync.conf` file must be the same on every node in the cluster. The command  `pcs cluster sync` provides a mechanism to sync the `corosync.conf` file from the current node to all other cluster nodes in the same [[Cluster|cluster]]. After synchronizing the corosync configuration file, the cluster can be started again with `pcs cluster start --all`.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[Cluster]], [[Red Hat High Availability Add-On]]