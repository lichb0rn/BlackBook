---
title: "PowerVault ME4, ME5: How to Collect Historical Disk Performance Statistics"
source: https://tools.jet.su/emc_kb/000227931/
author:
  - "[[Dell US]]"
published:
created: 2026-01-22
description:
tags:
  - clippings
related:
  - "[[СХД DELL-EMC ME5012 SN G66ZZQ3]]"
---
---

### Detailed Article

#### Instructions

Using a host on the management network, Microsoft Windows administrators can open a CMD or PowerShell prompt or Linux administrators can open a console. From the host CLI, use an SFTP application to open a connection on TCP port 1022 to PowerVault ME4 or ME5 series controller management IP address.

  
**Note:** FTP protocol can be used, however FTP is disabled by default and must be enabled on the PowerVault ME interface by a user with admin. Some host firewall configurations may block TCP port 21.

### Instructions for getting historical disk-performance statistics:

1. Log in as a user that has permission to use the FTP or SFTP interface.
2. Type the following command:
```
get perf[:<date/time-range>] <filename>.csv
```

Where `**<filename>.csv**` is the file to capture the historical disk-performance statistics and `**<date/time-range>**` is optional and specifies the time range of data to transfer, in the format: `**start.<yyyy>-<mm>-<dd>.<hh>:<mm>.[AM|PM].end.<yyyy>-<mm>-<dd>.<hh>:<mm>.[AM|PM]**`.

  
The `**<date/time-range>**` string must contain no spaces and must be in a 12-hour format.

  
Example:

```
get perf:start.2024-01-03.04:00.AM.end.2024-01-05.10:00.PM. statistics.csv
```
```
C:\>  sftp -P 1022 manage@10.0.0.1             (Note: -P is an uppercase letter)
<snip>Help text removed for brevity</snip>
Password:
Connected to manage@10.0.0.1.
sftp>  get perf:start.2024-08-19.01:00.AM.end.2024-08-19.10:00.PM. statistics.csv 
Fetching /perf:start.2024-08-19.01:00.AM.end.2024-08-19.10:00.PM. to statistics.csv
/perf:start.2024-08-19.01:00.AM.end.2024-08-19.10:00.PM.                              100%   79KB 846.4KB/s   00:00
sftp>  bye          (Note: use bye to exit SFTP/FTP application)
```

  
**Note:** The syntax used is important. An incorrect positioning of characters when specifying the date range may result in an error such as:

```
remote open("/perf:start.2024-08-19.01:00.AMend.2024-08-19.10:00.PM."): No such file or directory.
```
Based on this output message if the period (.) is missing, `**AMend**` must read `**AM.end**`.

  
Administrators should specify a recent 24-hour window covering the time period they want to review. The CSV file records disk I/O metrics taken at 15 minute intervals. Longer time ranges mean that the sample interval is less frequent.

#### Affected Products

OEMR ME40XX and ME4XX, Dell EMC PowerVault ME4012, Dell EMC PowerVault ME4024, Dell EMC PowerVault ME4084, Dell EMC PowerVault ME412 Expansion, Dell EMC PowerVault ME424 Expansion, PowerVault ME5012, PowerVault ME5024, PowerVault ME5084

https://tools.jet.su/emc_kb/000242285/

За разъяснениями - disk-hist-statistics в cli guide.
