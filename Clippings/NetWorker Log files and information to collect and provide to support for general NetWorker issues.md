---
title: "NetWorker: Log files and information to collect and provide to support for general NetWorker issues"
source: https://tools.jet.su/emc_kb/000079239/
author:
  - "[[Dell US]]"
published:
created: 2026-02-02
description:
tags:
up:
  - "[[NetWorker]]"
---
Article Number: 000079239

---

Audience Level: Internal

### Article Content

---

###### Symptoms

Note that technology is deterministic - by definition, something failing where it was previously working requires something to have changed. A newly implemented component with no working history is significantly different to troubleshoot.  
  
Obvious and identifiable changes:

- Software version or configuration change
- Hardware or transport change or reconfiguration
- Environmental events like power outages, transport failures, disk failures
Undetected changes
- Corruption of software resources or filesystems
- Conflicting operations on network, SAN or hosts
- Reconfiguration of transport or hosts by other teams
- Data volume or transport traffic increase
- Non-catastrophic environmental events which don't raise alerts

When preparing a problem for extended review and technical troubleshooting work, ensure the following general directives are observed. These items will ensure that sufficient data is collected mechanically, and that the correct questions are asked to properly qualify the issue.

###### Cause

Define the problem clearly:

- **WHAT** is the operation or attribute which is failing, deviant, or is the subject of questions? What details of the failure sequence are available?
- **WHICH** specific components and data paths are involved, e.g. binaries, SAN / network switches? Software versions? Storage types or instances?
- **WHERE** in the normal workflow does the problem occur? If the same operation is attempted using a different workflow, do results differ?
- **WHEN** did the problem first occur? How long does it last? What dates/times has it occurred since? Have recent changes been identified?
- **HOW** does the problem occur: consistently or intermittently? How is the problem alleviated after it occurs?
- **WHO** are the hosts involved in the problem, and what are their properties (NetWorker host type, NetWorker version, name, IP, OS, CPU etc.)?
- **WHY** are some components affected, when similar components are not? What differences exist between unaffected but like components?

###### Resolution

### GENERIC LOGS

Most NetWorker logs can be collected from Windows and Linux NetWorker servers, storage nodes, and/or clients using the NSRGET utility. The utility can be downloaded from:

[https://central.dell.com/solutions/Networker-Tools](https://central.dell.com/solutions/Networker-Tools)

  
1\. Extract the NSRGET utility to any temporary directory  
2\. Instructions on how to use NSRGET can be found in: [NetWorker: How to Use the NSRGet NetWorker Data Collection Tool](https://tools.jet.su/emc_kb/000022799/index.html)  
  
The following KB details logs used by NetWorker: [NetWorker: Log Files and Locations](https://tools.jet.su/emc_kb/000004080/index.html)  
  
Collect the following from **all involved NetWorker hosts**, (including Server and Storage Nodes):

- **NetWorker debug files:** directory listing of \[nsr\]/debug
	- This directory should be empty. If there are files under /nsr/debug which coincide with the date an issue arose, it could be indicative of a problem.
- **NetWorker core files:**
	- Linux: /nsr/cores
	- Windows: C:\\Program Files\\EMC NetWorker\\nsr\\cores
- **NetWorker app logs:** zip of \[nsr\]/apps; zip of \[nsr\]/applogs; zip of \[nsr\]/rmagentps/logs; bundle of \[nsr\]/logs/lib\*, nsrbr\*, nsrsnap\*\*
- **NetWorker logs:** \[nsr\]/logs/daemon.raw, \[nsr\]/logs/networkr.raw
	- [NetWorker: How to use nsr\_render\_log](https://tools.jet.su/emc_kb/000022793/index.html)
	- [NetWorker: How to automatically render daemon.raw to daemon.log in real time](https://tools.jet.su/emc_kb/000023670/index.html)
- **NetWorker client configuration:** zip of \[nsr\]/res/nsrladb, \[nsr\]/res/servers file (may not exist), \[nsr\]/res/nsrdb (if NetWorker server)
	- These are collected by the NSRGET utility.
- **Startup script:** Solaris & Linux - /etc/init.d/networker, HPUX - /sbin/init.d/networker
- **Backup policy logs:**
	- Linux: /nsr/logs/policy/ *POLICY\_NAME* / *WORKFLOW\_NAME*
	- Windows: C:\\Program Files\\EMC NetWorker\\nsr\\logs\\policy\\ *POLICY\_NAME* \\ *WORKFLOW\_NAME*
- **NetWorker version and build**: [NetWorker: Methods for Identifying NetWorker Software version](https://tools.jet.su/emc_kb/000197614/index.html)
- Known patches installed for NetWorker
- Operating system, Edition, Patch Level, CPU and bit-width (32/64 bit)
	- Linux: cat /etc/\*release; uname -m
	- Windows: systeminfo | findstr "OS Type"
	- NSRGET or EMCREPORTS will also detail the OS version and system architecture.
- EMC Reports utility: [https://www.dell.com/support/home/en-us/product-support/product/emcreports/drivers](https://www.dell.com/support/home/en-us/product-support/product/emcreports/drivers)
	- EMC Reports collects additional host information including full OS details and configuration, operating system messages or event logs; some of this information is also collected in NSRGET; whereas EMC Reports is more operating specific logs. EMC Reports can be collected in conjuction with NSRGET or on a system which may not have a NetWorker client software installed; for example, a VMware Virtual Machine backed up by vProxy.
- **Core dumps:** [NetWorker: Troubleshooting Process Core Dumps](https://tools.jet.su/emc_kb/000128100/index.html)
- **For suspected name resolution issues:** [NetWorker: Name Resolution Troubleshooting Best Practices](https://tools.jet.su/emc_kb/000079462/index.html)
  
Collect the following from the **NetWorker Server** only:
- **NetWorker resource database:** Zipped copy of \[nsr\]/res/nsrdb
- **NetWorker media database:**[How To Export the NetWorker Media Database Using nsrmmdbasm](https://tools.jet.su/emc_kb/000032989/index.html)
- NSRGET will collect most logs needed; however it will not collect:
	- AUTHC (authentication) logs:
		- Linux: /nsr/logs/authc
		- Windows: C:\\Program Files\\EMC NetWorker\\nsr\\authc-server\\tomcat\\logs
	- NetWorker Management Console (NMC) (gstd) logs:
		- Linux: /opt/lgtonmc/logs/
		- Windows: C:\\Program Files\\EMC NetWorker\\Management\\GST\\logs
	- NetWorker Web User Interface (NWUI) logs:
		- Linux: /opt/nwui/logs
		- Windows: C:\\Program Files\\EMC NetWorker\\nwui\\logs
Collect the following from any **NetWorker Storage Node** (including Server):
- **NetWorker discovery command:**inquire -lc output
- **NetWorker bus interrogation:**lusbinfo / lusbinfo -v output
- **NetWorker SJI command outputs:**sjisn \[x.y.z\], sjirdtag \[x.y.z\], sjirjc \[x.y.z\] (where x.y.z is SCSI address OR device file handle)
- **NetWorker CDI command outputs:**cdi\_inq -f \[dev\] -v, cdi\_get\_config -f \[dev\] -v, cdi\_get\_status -f \[dev\] -v, cdi\_get\_blocksize -f \[dev\] -v (where dev is device file handle)
- **NetWorker device and mount state summary:**nsrmm
- **NetWorker simple autochanger output:**nsrjb -C \[jukebox\_name\]
- **NetWorker disk details:** recursive directory listings for any affected AFTD/DD/FTD structure, as well as details of the disk device and its connection method to host.
- Operating system, Edition, Patch Level, CPU and bit-width (32/64 bit)
	- Linux: cat /etc/\*release; uname -m
	- Windows: systeminfo | findstr "OS Type"
	- NSRGET or EMCREPORTS will also detail the OS version and system architecture.
- NSRGET and/or EMC Reports are recommended for support engagements.
**Note:** The above device commands, as well as OS device commands listed below, may cause SCSI resets if used on active devices. Use only as needed when all tape devices attached to the system, or those specified, are idle **across all host instances.**  
  
Collect the following from any affected **NetWorker License Manager** Host:
- Licensing command output: nsrlic -C
- **NetWorker License database:** zip of \[nsr\]/res/lgtolm.res, \[nsr\]/res/lictype.res, \[nsr\]/logs/lgtolmd.log, \[nsr\]/logs/license\*
Collect the following from any affected **NetWorker Management Console** Host:
- Operating system, Edition, Patch Level, CPU and bit-width (32/64 bit)
	- Linux: cat /etc/\*release; uname -m
	- Windows: systeminfo | findstr "OS Type"
	- NSRGET or EMCREPORTS will also detail the OS version and system architecture.
- Management Console Log (gstd.raw - ideally, rendered):
	- Linux - /opt/lgtonmc/logs
	- Windows - \[Install path\]\\Management\\GST\\logs
	- [NetWorker: How to use nsr\_render\_log](https://tools.jet.su/emc_kb/000022793/index.html)
- NMC version including build number
	- [NetWorker: Methods for Identifying NetWorker Software version](https://tools.jet.su/emc_kb/000197614/index.html)
- Oracle Java JRE version: [https://www.java.com/en/download/help/version\_manual.html](https://www.java.com/en/download/help/version_manual.html)
- NetWorker Runtime Environment (NRE):
	- Linux:
		- rpm -qa | grep nre
		- /opt/nre/java/latest/bin/java -version
	- Windows:
		- Java version will be listed under: C:\\Program Files\\NRE\\java\\ **jre#.#.#\_###**
			- If multiple Java folders are listed check **S** **ystem Environment Variable JAVA\_HOME**  or  **NSR\_JAVA\_HOME** for which path is currently used by NetWorker
		- NRE version will be listed from **Control Panel**, under  **Programs and Features**
- **Java Webstart file:** \[nmc\]/web/gconsole.jnlp
- **NMC configuration file**: \[nmc\]/etc/gstd.conf
NetWorker VMware Protection (NVP) vProxy Appliance:
- Log bundles: [NVP-vProxy: How to collect bundle for vProxy](https://tools.jet.su/emc_kb/000022831/index.html)
- ProxyHC (Health Check) Tool: [NVP-vProxy: How to use health check tool ProxyHC on vProxy appliance](https://tools.jet.su/emc_kb/000022590/index.html)

###### Internal Notes

NetWorker SharePoint Page: [https://dell.sharepoint.com/sites/NetWorkerSupportTeam](https://dell.sharepoint.com/sites/NetWorkerSupportTeam)  
NetWorker Confluence: [https://confluence.cec.lab.emc.com/display/NWOP/NetWorker](https://confluence.cec.lab.emc.com/display/NWOP/NetWorker)  
NetWorker Compat. Matrix: [https://elabnavigator.dell.com/eln/modernHomeAutomatedTiles?page=NetWorker](https://elabnavigator.dell.com/eln/modernHomeAutomatedTiles?page=NetWorker)  

#### Article Properties

---

###### Affected Product

NetWorker

###### Product

NetWorker Series

###### Last Published Date

26 Sep 2023

###### Version

4

###### Article Type

Solution