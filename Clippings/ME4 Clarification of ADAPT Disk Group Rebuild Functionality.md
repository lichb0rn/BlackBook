---
title: "ME4: Clarification of ADAPT Disk Group Rebuild Functionality"
source: "https://tools.jet.su/emc_kb/000190176/"
author:
  - "[[EMC]]"
published:
created: 2025-11-24
description:
tags:
  - "clippings"
---
---

### Detailed Article

#### Symptoms

Although the ME4 Administrator's Guide describes ADAPT disk group features and functionality, the implications of protection from multiple failed drives is not clearly spelled out.

#### Cause

ADAPT disk groups are virtual RAID 6 with the minimum configuration of 12 drives. Having a default of two drives' worth of spare capacity based on the size of the largest disk in the group. 80% of the remaining group capacity is dedicated to user data space with 20% for parity.  
  
Given the amount of reserved capacity, an ADAPT disk group can tolerate up to two drive failures at any one time and still rebuild to from the parity to the reserved spare capacity. See [PowerVault ME4 Series ADAPT Software](https://www.delltechnologies.com/asset/nl-be/products/storage/industry-market/powervault-me4-series-adapt-software-white-paper.pdf), page 9 for a discussion of the priority of rebuilds in a two-drive failure scenario.  

#### Resolution

Over time an ADAPT disk group can continue to rebuild and recover from more than two sequential drive failures if all the follow is true:

- No more than two drives have failed simultaneously.
- Rebuilds of the ADAPT disk group have completed and the group is online.
- The ADAPT disk group has unused/reserved capacity equal to or greater than the total capacity of the failed drive.
Note: in an optimal state, an ADAPT disk group has a redundancy of two drives (parity) and a maximum reserved spare capacity equal to two times the largest capacity drive in the group.  
  
Spare capacity greatly depends on operations active on the disk group as well. Active rebuilds consume capacity which may cause spare capacity to be insufficient until spare disks are replaced or more disks are added. If this occurs the disk group shows a Degraded state.  
  
Drives can be added to expand the ADAPT disk group. This will:
- Replenish the current reserved spare capacity and/or add to the current free capacity.
- Increase user data capacity of the ADAPT disk group.
NOTE: The reserved spare capacity of the ADAPT disk group will not be modified. It remains at the equivalent of 2x of the largest capacity drive if the disk group is fully redundant.  
  
Also when expanding an ADAPT disk group:
- Capacity from drives added is first used to meet spare capacity requirements.
	- If there is space remaining, then usable capacity is expanded.
- Expansion of the ADAPT disk group does not change reserved spare capacity: It remains at 2x the capacity of the largest disk in the group.
- If a larger disk or disks are added to an existing ADAPT disk group, the actual spare capacity increases to meet the requirement of maintaining a spare capacity of 2x the largest disk in the group.

#### Affected Products

ME Series, OEMR ME40XX and ME4XX, Dell EMC PowerVault ME4012, Dell EMC PowerVault ME4024, Dell EMC PowerVault ME4084