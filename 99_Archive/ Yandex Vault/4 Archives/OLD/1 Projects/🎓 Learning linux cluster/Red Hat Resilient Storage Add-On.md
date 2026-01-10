---
uuid: 20230825153751
created: 2023-08-25T15:37:51
alias:
---

# [[Red Hat Resilient Storage Add-On]]

In order to provide cluster services with the Red Hat High Availability Add-on, multiple software  components are required on the cluster nodes:

- [[corosync]]: This is the framework used by [[Pacemaker]] for handling communication between the  cluster nodes. [[corosync]] is also Pacemaker’s source of membership and quorum data.
- [[pcs]]:  The pcs RPM package contains two cluster configuration tools: 
	- 1. The [[pcs]] command provides a command-line interface to create, configure, and control every aspect of a Pacemaker/Corosync cluster.  
	- 2. The [[pcsd]] service provides the cluster configuration synchronization and a web   front end to create and configure a Pacemaker/Corosync cluster.
- [[Pacemaker]]:  This is the component responsible for all cluster-related activities, such as monitoring cluster membership, managing the services and resources, and fencing cluster members.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[Cluster]], [[High-availability]]