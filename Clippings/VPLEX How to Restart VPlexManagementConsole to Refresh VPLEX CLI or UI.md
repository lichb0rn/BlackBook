---
title: "VPLEX: How to Restart VPlexManagementConsole to Refresh VPLEX CLI or UI"
source: "https://tools.jet.su/emc_kb/000040517/"
author:
  - "[[Dell US]]"
published:
created: 2026-02-06
description:
tags:
  - "clippings"
---
Article Number: 000040517

---

Audience Level: Internal

### Article Content

---

###### Symptoms

- VPLEX UI or CLI does not display up-to-date information.
- VPLEX UI or CLI has conflicting information
- VPLEX UI or CLI has been slowing down
- Unable to log in to VPLEX CLI or UI

###### Cause

The management-console process could be hung or slow to respond due to memory issues and may need to be restarted.

###### Resolution

Follow the steps below to restart the VPlexManagementConsole service. The VPlexcli and UI are refreshed by restarting this service.  
  
**Note:** If the VPLEX is running GeoSynchrony 6.2 SP1 or higher, you must use the alternate steps in the section below titled, *" [Restarting VPlexManagementConsole on GeoSynchrony 6.2 SP1 and later code levels](https://tools.jet.su/emc_kb/000040517/#6.2SP1)."* Otherwise, if VPLEX is running GeoSynchrony 6.2 P7 or lower, use the below steps to restart the console service.

### Restarting VPlexManagementConsole on GeoSynchrony 6.2 P7 and lower code levels

1. Log in to the management server using PuTTY and the service account credentials.
2. Once on the management server, run the following command.
```
service@ManagementServer:~> sudo /etc/init.d/VPlexManagementConsole restart
Restarting EMC VPlex Management Console...
```
1. When the service has restarted, check the status of the service to ensure it is running using the command below.
```
service@ManagementServer:/etc/init.d/> sudo /etc/init.d/VPlexManagementConsole status
VPlexManagementConsole is running (pid 12345)
```
1. After restarting the management console, allow approximately five minutes for the system to stabilize before attempting a new login. The wait time varies depending on the size of the VPLEX environment.
2. Access the UI by opening a browser and typing in the management server IP address or access the VPlexcli level from the management server. Check to see if the changes that you were not able to see before, as noted in the Symptoms section, now show.
3. Access the VPLEX UI:
```
https:// <mgmt server ip address>
```

Or  
Access the VPlexcli from the management server:

```
service@ManagementServer:~> vplexcli
```

### Restarting VPlexManagementConsole on GeoSynchrony 6.2 SP1 and later code levels

Starting in GeoSynchrony 6.2 SP1, most of the existing Linux processes are now managed through the *systemctl* command, and as such you must use this new command format in order to start, stop, restart, or check the status on a service.  
1. To restart the VPlexManagementConsole service, run the following command:
```
service@ManagementServer:~> sudo systemctl restart VPlexManagementConsole
```
1. To check status on the VPlexManagementConsole service, run the following command:
```
service@ManagementServer:~> sudo systemctl status VPlexManagementConsole
```
1. After restarting the management console, allow approximately five minutes for the system to stabilize before attempting a new login. The wait time varies depending on the size of the VPLEX environment.

  
Example of the output seen when the status of the VPlexMaanagementConsole service is checked..

```
service@ManagementServer:~> sudo systemctl status VPlexManagementConsole
● VPlexManagementConsole.service - VPlexManagementConsole
     Loaded: loaded (/etc/systemd/system/VPlexManagementConsole.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-06-17 10:23:51 UTC; 3 weeks 4 days ago
    Process: 18961 ExecCondition=/bin/bash -c [ "$(cat /proc/platform)" == "snowhill" ] || [ "$(cat /proc/spid)" == "0" ] (code=exited, status=0>
    Process: 18964 ExecStartPre=/bin/bash -l -c echo /usr/bin/java $JAVA_OPTS -cp $CLASSPATH com.emc.vplex.smsv2.cli.Main $CLI_OPTS (code=exited>
   Main PID: 18985 (java)
      Tasks: 422
     CGroup: /system.slice/VPlexManagementConsole.service
             ├─18985 /usr/bin/java -Xmx2048m -XX:+UseMembar -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/var/log/VPlex/cli//vplex-oome-heap>
             ├─19408 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─19414 ssh: /tmp/ssh-ctrl-service@128.221.252.35:22 [mux]
             ├─19415 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─19418 ssh: /tmp/ssh-ctrl-service@128.221.252.36:22 [mux]
             ├─19430 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─19436 ssh: /tmp/ssh-ctrl-service@128.221.252.67:22 [mux]
             ├─19437 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─19440 ssh: /tmp/ssh-ctrl-service@128.221.252.68:22 [mux]
             ├─21115 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─21118 ssh: /tmp/ssh-ctrl-service@128.221.253.35:22 [mux]
             ├─21122 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─21125 ssh: /tmp/ssh-ctrl-service@128.221.253.36:22 [mux]
             ├─21130 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             ├─21133 ssh: /tmp/ssh-ctrl-service@128.221.253.67:22 [mux]
             ├─21142 ssh -p 22 -t -oBatchMode=yes -oControlMaster=auto -oControlPersist=yes -oControlPath=/tmp/ssh-ctrl-%r@%h:%p -oServerAliveIn>
             └─21145 ssh: /tmp/ssh-ctrl-service@128.221.253.68:22 [mux]

Jul 12 13:20:06 ManagementServer sudo[30096]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:06 ManagementServer sudo[30121]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:06 ManagementServer sudo[30119]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:06 ManagementServer sudo[30147]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:06 ManagementServer sudo[30156]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:07 ManagementServer sudo[30183]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:07 ManagementServer sudo[30195]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:20:25 ManagementServer sudo[30298]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:23:46 ManagementServer sudo[32697]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
Jul 12 13:23:46 ManagementServer sudo[32709]:  service : PWD=/var/log/VPlex/cli ; USER=root ; COMMAND=/usr/sbin/ipsec status
lines 1-36/36 (END)
```

Note: To get back to the management server prompt after the above output is displayed press Ctrl-c.

1. Access the UI by opening a browser and typing in the management server IP address or access the VPlexcli level from the management server. Check to see if the changes that you were not able to see before, as noted in the Symptoms section, now show.

Access the VPLEX UI:

```
https:// <mgmt server ip address>
```

Or

Access the VPlexcli from the management server:

```
service@ManagementServer:~> vplexcli
```

###### Additional Information

**NOTE:** After restarting the VPlexManagementConsole, the VPLEX CLI and UI requires at least 1-5 minutes for the VPLEX to stabilize before logging back in.

- If you attempt to log in to the VPlexcli immediately after restarting the VPlexManagementConsole, the login attempts fail and can possibly have false-positives while the information is refreshed in the CLI and UI.
- If a message is displayed stating that the process could not be gracefully stopped, run the command to restart the VPlexManagementConsole again.

**NOTE:** If Watch4Net is running on the VPLEX, the wait period after restarting the VPlexManagementConsole can take up to five minutes before you can access the VPlexcli again.

  
![](https://www.youtube.com/watch?v=0onOTEOG_mk)  

**NOTE:** The knowledge base article video maybe out of date with the content of the knowledge base article, Dell does plan to bring back Video knowledge base articles and once available all knowledge base articles with older videos will be updated.

#### Article Properties

---

###### Affected Product

VPLEX GeoSynchrony, VPLEX Series

###### Last Published Date

24 Jul 2024

###### Version

7

###### Article Type

Solution