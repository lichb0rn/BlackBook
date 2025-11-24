---
title: "ME4:  Disk group offline after multiple drive failures"
source: https://tools.jet.su/emc_kb/000190954/
author:
  - "[[EMC]]"
published:
created: 2025-11-24
description:
tags:
  - clippings
---
Article Number: 000190954

---

Audience Level: Internal

### Article Content

---

###### Symptoms

During operation the ME4 may report a drive failure with the following message.  

```
58 Error
An error was reported by a disk drive. (disk: channel: 1, ID: 129, SN: ZL2FEZCG, enclosure: 1, slot: 1)
(Key,Code,Qual,UEC:0x4,0x80,0x86,0x0000) (CDB:Rd 64aa7908 02f8)(Info:0x64AA7BFF)(CmdSpc:0x0, FRU:0x3, SnsKeySpc:0x0)(Hardware, no decode for ASC/ASCQ)
```

###### Cause

This is an issue in the firmware of the following Seagate families of drives, Tatsu, Mobula, MobulaBP and Evans drives.  
  
Root Cause:

- IOEDC read error detected near the end of transfer and the error LBA is outside of the command LBA range.
- The workload was a sequential read workload that triggered hardware streaming, but with occasional backward skips. During the read operation in this case, the decryption hardware may incorrectly prefetch the data outside of command range when the hardware is reloaded for a new burst with incorrect sector count.
- The read data may not be available from the media during the prefetch and hence the IOEDC check could fail.

###### Resolution

Resolution actions:  
  
**1) Before any reconstruction starts, update every non-failed drive to ESL5/CSLB.**  
  
2) The failed drives can be brought back online by either forcing a rescan disk channels using the System Action drop down in the GUI. If this doesn't bring the drive back it may require you to pull the drive out of the Array wait a couple of minutes and then re-insert the drive and wait for the Array which should bring the drive back online.  
  
3) Once reconstructions are finished update remaining drives to ESL5/CSLB, currently we only have firmware for the Seagate Evans family.  
  
***Note: Firmware for the Mobula drives is coming at a later time. Step 1 will still apply to bring drive back online now, and I will update this LKB when the firmware becomes available for use.***  
  
Latest HDD/SDD FW Bundle is [A23](https://www.dell.com/support/home/en-my/drivers/driversdetails?driverid=x3m99&oscode=wst14&productcode=powervault-me4024). Fix for Cimarron and Mobula BP released at the end of December.

###### Internal Notes

**For data unavailable (DU) events.**

When a disk group is offline or in a quarantine state do not clear disk metadata from other disks that may be offline. Doing this before the disk groups have been recovered will remove any chance of recovery. If you are unsure how to proceed please engage your next level of support.

Do not switch off or on arrays as a first step without understanding the problem, doing so may remove the possibility of root causing the failure as log runtime data is not saved and it may delay or prevent recovery efforts.

In event of a data unavailable situation please gather the following information:

1. Generate the latest support bundle from the ME array and attach to case or OLA.
2. Is production impacted?
3. When was the last successful backup of data on the array?
4. Outline what steps (if any) have been taken by the customer or support to try and recover.
5. IOEDC fix Seagate disks firmware is currently undergoing testing. If you have a customer with multiple disk down due to issues mention here-in, pls open a PSE or Contact IPS to get pre-released copy of the firmware.
  
I general we will want to know the following from the support bundle.
1. Circumstances that led up to the DU event
2. From the event logs why the drives are offline (usually SCSI sense code data)
3. Drive models in use.
4. Disk group configuration.
5. Last drive to fail.
6. If enclosures (ME412, ME424, ME484) are attached are they cabled correctly.
7. Any other system health issues.

PSE-16583, PSE-16491, PSE-16516, [JIT-216118](https://jira.gtie.dell.com/browse/JIT-216118 "Seagate Drive ST4000NM017A going offline with Sense 04/80/86"), [JIT-215158](https://jira.gtie.dell.com/browse/JIT-215158 "Seagate drive ST8000NM014A Logs review"), PSE-16722;

#### Article Properties

---

###### Affected Product

Dell EMC PowerVault ME4012, Dell EMC PowerVault ME4024, Dell EMC PowerVault ME4084

###### Product

ME Series

###### Last Published Date

08 Mar 2023

###### Publish Status

Online

###### Version

6

###### Article Type

Solution