---
uuid: 20230901110536
created: 2023-09-01T11:05:36
aliases:
  - кворум
---

# [[Quorum]]

## What is Quorum?
In order for a [[cluster]] to work as expected, the nodes must be in agreement on certain facts, such as  which machines are currently cluster members, where services are running, and which machines are  using which resources.  

The method in which this is implemented in the [[Red Hat High Availability Add-on]] is by the use of a majority voting scheme. Every cluster node casts one vote if it successfully joins the [[corosync]] network communication and is able to communicate with the other nodes that are already participating in the cluster.  

The cluster is operational if more than half of all possible votes are successfully cast. The minimum  number of votes needed to achieve more than half of the votes is called the quorum. If quorum is achieved, the cluster is considered **quorate**. **A cluster loses quorum if half of the nodes or more cannot communicate with each other**.

When a cluster gets started, all cluster nodes try to communicate with each other and aim to achieve quorum. As soon as a majority is formed, there is a quorate cluster. All other **nodes that have not successfully joined the quorate cluster get [[Cluster Node Fencing|fenced]] by a node that has quorum**. If a node that is part of the quorate cluster is not able to communicate with the cluster anymore, the node gets fenced.

## Split-brain
This situation, where two halves of a cluster operate independently from each  
other, is referred to as a split-brain.

**Split-brain is a particular concern in two-node clusters**, since if either node fails, the other node does  not consist of a majority of the nodes in the cluster. Special steps need to be taken to allow two-node cluster operation and still avoid split-brain.

## Calculating quorum
Quorum is calculated and managed in the Red Hat High Availability Add-on by the [[corosync]] component `votequorum` . The `votequorum` component uses two values to calculate if the cluster is quorate:  
1. **Expected votes**: The number of votes expected if all cluster nodes are fully operational and communicating with each other.  
2. **Total votes**: The number of votes currently present. This can be lower than the number of  expected votes if some nodes are not up or not communicating with the cluster.  

The number of votes required to achieve quorum is based on **Expected Votes** . The following formula  shows how many votes are required for quorum.
$$
Quorum = floor(\frac{expected\ votes}{2} + 1)
$$

## Displaying quorum status
The [[Red Hat High Availability Add-on]] provides a comprehensive utility to display the current state of quorum in a cluster: `corosync-quorumtool`. The `corosync-quorumtool` provides an overview of  quorum-related information, such as **Total Votes** and **Expected Votes** , and shows if the cluster is  quorate at a glance.
```shell
[root@node1 ~]# corosync-quorumtool
Quorum information
------------------
Date:             Fri Sep  8 10:57:32 2023
Quorum provider:  corosync_votequorum
Nodes:            3
Node ID:          1
Ring ID:          1/205
Quorate:          Yes

Votequorum information
----------------------
Expected votes:   3
Highest expected: 3
Total votes:      3
Quorum:           2
Flags:            Quorate

Membership information
----------------------
    Nodeid      Votes Name
         1          1 192.168.0.201 (local)
         2          1 192.168.0.202
         3          1 192.168.0.203
```

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[High-availability]], [[Cluster]]