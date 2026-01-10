---
uuid: 20230825152146
created: 2023-08-25T15:21:46
alias:
---

# [[High-availability clusters]]

The major goal of a high-availability cluster is to keep services as available as possible by eliminating  bottlenecks and single points of failure. A high-availability cluster uses various concepts and  techniques, which allow for service integrity and availability:

## Resources and resource groups. 
In clustering terminology, **the basic unit of work is called a  resource**. A single IP address, filesystem or database would all be considered resources. Typically, relationships between these resources are defined to create user-facing services. One of the most  common ways to define these relationships is to **combine a set of resources into a group**. This  specifies that all resources in the group need to run together on the same node and establishes a  fixed (linear) start and stop order.

## Failover. 
High-availability clusters try to keep services available by migrating them to another node  when the cluster notices that the node that was originally running the service is not responding.

## Fencing. 
Fencing is a mechanism that ensures a malfunctioning cluster node can not cause  
corruption, so that its resources can be safely recovered elsewhere in the cluster. This is necessary  because we cannot assume that an unreachable node is actually off. Fencing is often accomplished  by powering the node off.

## Shared storage. 
Most high-availability clusters will also need a form of shared storage, or storage  that can be accessed from multiple nodes. Shared storage provides the same application data to  multiple nodes in the cluster. The data may be accessed either sequentially or simultaneously by an  application running on the cluster. A high-availability cluster needs to ensure data integrity on the  shared storage. **Data integrity is guaranteed by [[Cluster Node Fencing|fencing]].**

## Quorum. 
[[Quorum]] describes a voting system that is required to maintain cluster integrity. Every  cluster member has an assigned number of votes; by default, one vote. Depending on the cluster  configuration, the cluster gains quorum when either half of the votes or more than half of the votes  are present. Cluster members that fail to communicate with other cluster members and cannot send  their votes are fenced by the majority of the cluster members that operate as expected. A cluster  normally requires quorum to operate.

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[Cluster]], [[High-availability]]