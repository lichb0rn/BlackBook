---
uuid: 20230825150942
created: 2023-08-25T15:09:42
alias:
- кластер
---

# [[Cluster]]

A cluster is a set of computers working together on a single task. Which task is performed, and how  that task is performed, differs from cluster to cluster.

- [[High-availability clusters]]: The goal of a high-availability cluster, also known as an HA cluster or  failover cluster, is to keep running services as available as they can be. This is primarily achieved by having the nodes of the high-availability cluster monitor each other for failures, and  migrating services to a node that is still considered "healthy" when a service or node fails. 
	- Highavailability clusters can be grouped into two subsets:  
		- **Active-active** high-availability clusters, where a service runs on multiple nodes, thus leading to shorter failover times.  
		- **Active-passive** high-availability clusters, where a service only runs on one node at a time.
		Examples of software that implement high-availability clustering are [[Pacemaker]], and the [[Red Hat High Availability Add-On]].
- [[Storage clusters]]: In a storage cluster, all members provide a single cluster file system that can  be accessed by different server systems. The provided file system may be used to read and  write data simultaneously. This is useful for providing high availability of application data, like  web server content, without requiring multiple redundant copies of the same data. An example  of a cluster file system is [[GFS2]] , which is provided by the [[Red Hat Resilient Storage Add-On]].

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[100 General IT]]