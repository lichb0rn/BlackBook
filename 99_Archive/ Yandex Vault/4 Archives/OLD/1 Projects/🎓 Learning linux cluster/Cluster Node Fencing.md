---
uuid: 20230829153035
created: 2023-08-29T15:30:35
alias:
---

# [[Cluster Node Fencing]]

Fencing is a requirement for any high-availability [[Cluster]]. Fencing prevents data corruption from an errant node. Fencing also isolates and restarts a cluster member if the node fails to join the cluster and the remaining cluster members are still quorate. Depending on the hardware used, it can fence a node by turning off the network connection to the shared storage or by power-cycling the node.

The first step to set up fencing is to set up the physical fencing device. There are different hardware devices that are capable of fencing cluster nodes, such as:  
- Uninterruptible power supply (UPS)  
- Power distribution unit (PDU)  
- Blade power control devices  
- Lights-out devices

For virtual machine fencing, each cluster node requires its own fence device. This gets accomplished with the `pcs stonith create` command:
```shell
pcs stonith create DemoFence fence_virt pcmk_host_list=192.168.0.201,192.168.0.202,192.168.0.203
```

The `pcs stonith show` command shows the status of the fence devices that are attached to the [[Cluster]]. All fence devices should show a status of `Started` .
If the status of one or more fence devices is `Stopped` , there is most likely a problem in the  communication between the fencing agent and the fencing server. Verify the settings of the fence device with `pcs stonith show fence_device` .

To fence node:
```shell
[root@nodea ~]# pcs stonith fence nodeb.private.example.com
```
## Fencing mechanism
There are two main methods of fencing: **power fencing**, also known as *Shoot The Other Node In The  Head (STONITH)*, and **fabric fencing**. Both fencing methods require a fence device, such as a power  switch or the virtual fencing daemon and fencing agent software to enable communication between  the cluster and the fencing device. The fencing agent communicates when a particular node should  be fenced.

Fencing methods can be combined. When a node needs to be fenced, one fence device can cut off  [[Fibre Channel]] by blocking ports on a [[Fibre Channel]] switch, and an ILO card can then power cycle the  offending machine. Multiple fencing methods can act as a backup for each other. For example, the  cluster nodes are first fenced by power fencing, but if that fails, with fabric fencing.

---

## 📇 Additional Metadata
- 🛠️ Status:: #📚 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[High-availability clusters]]