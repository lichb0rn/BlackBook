---
title: "VPLEX: How to manually re-create the security certificates after expiring, forgetting the passphrase, the VPN certificates need to be re-created, or getting the SSL exception error"
source: "https://tools.jet.su/emc_kb/000169421/index.html#section_F"
author:
  - "[[Dell US]]"
published:
created: 2026-02-06
description:
tags:
  - "clippings"
---
Article Number: 000169421

---

Audience Level: Internal

### Article Content

---

###### Symptoms

These are reasons that the security certificates may need to be renewed or re-created manually:  

- Host certificate is going to expire\* orhas expired.
- VPN certificates must be manually re-created.
- NDU Pre-check reports SSL exception errors or Sun Security Errors.
- User forgets Certificate Passphrases.
\*Note: refer to the second note in the Resolution section about what you can do when a certificate is reported that it is going tp expire.

###### Cause

- Certificates are going to expire or have expired.
- User does not remember Certificate Passphrase.
- VPN tunnel goes down due to expired certificates  
	and a link drop occurred after the certificates expired.

###### Resolution

If the certificates have not yet expired, please refer to KBA 000158316, " [VPLEX: How to Renew Security Certificates](https://tools.jet.su/emc_kb/000158316/index.html) "

To check the expiry dates of the three certificates run each of the commands listed below from the management server prompt and note the date listed in the line "Not After: Month day HH:MM:SS Year GMT". This is the date the certificate will expire.  
  
The Host and webServerHost certificates each have a two-year duration:

**Host Certificate**:  
**openssl x509 -in /etc/ipsec.d/certs/hostCert.pem -noout -text | grep -A2 "Validity"**  
Validity  
Not Before: Sep 2 19:18:39 2021 GMT  
**Not After:** Sep 1 19:18:39 2022 GMT **<-- note this date**  
  
**webServerHost Certificate:**  
o **penssl x509 -in /etc/ipsec.d/certs/webServerHostCertFile.pem -noout -text | grep -A2 "Validity"**  
Validity  
Not Before: Sep 2 19:18:52 2021 GMT  
**Not After:** Sep 1 19:18:52 2022 GMT **<-- note this date**  
  
The CA certificate has a five-year duration:

**CA Certificate:  
openssl x509 -in /etc/ipsec.d/cacerts/strongswanCert.pem -noout -text | grep -A2 "Validity"**  
Validity  
Not Before: Sep 2 19:17:25 2021 GMT  
**Not After:** Sep 1 19:17:25 2026 GMT **<-- note this date**

Note: This KB is to be used when [ETA 194960: VPLEX: VPLEX Security Certificates for Host and Web Server Host expire prior to VPN Host](https://tools.jet.su/emc_kb/000154503/index.html) is encountered and the VPN link drops, the user cannot access or see the remote clusters and the Desktop/Online SolVe procedure for renewing certificates fails to work due to the VPN being down between the clusters (VPLEX Metro only) because of a link drop.  
  
**User forgot Certificate Passphrases**:  
There are four scenarios where the user may have forgotten Certificate Passphrases:  

- While creating the host certificate.
- While creating the web server host certificate.
- While configuring the VPN to the Cluster Witness Server from the Management Server.
- While configuring the VPN between the management servers the user forgot the passphrase of the local host certificate.

  
Follow the steps below to correct this issue. Even after following the steps below, if the issue persists, contact your local field representative for technical assistance and quote this article ID. If a local field representative is not available, contact the Dell Customer Support Center and mention this article.  
  
**Certificates are going to expire or have expired:**  
  
This KB also covers what to do when any certificate is about to expire\* or has expired.  

### Follow the steps below to renew all certificates at the same time before their expire.

\--------------------------------------------------------------------------------------------------------------------------------------------  
\*Note: If you received an e-mail alert that the certificates will expire in seven days (pre-6.x), or one month or 30 days, (6.x and later), and this time period has not yet passed first follow the actions covered in the VPLEX Procedure "Renew security certificates" which can be found on the VPLEX SolVe Desktop or [SolVe Online](https://solve.dell.com/solve/home/46) Procedure Generator under,  
  
VPLEX > Admin > Admin procedures > Manage > Renew security certificates

![image.png](https://tools.jet.su/emc_kb/000169421/ka06P000000oT9mQAE_en_US_1.jpeg)  
  
Be sure to select the procedure that applies to the VPLEX configuration you have and if Cluster Witness is configured on the VPLE-Metro select that procedure.

  
**If you are running GeoSynchrony 6.2 Patch 5 and later you can go to the GUI and in the Dashboard > SYSTEM STATUS screen. For the actions to take in the GUI please see the selection listed below.**  

If after attempting to follow the actions in the procedure, or at the GUI, you are unable to renew the certificates then follow the appropriate section in this KBA per the code version running on the VPLEX to re-create the security certificates.  
\--------------------------------------------------------------------------------------------------------------------------------------------

**VPN certificates must be manually re-created:**  
This KBA can also be used when any certificate is about to expire (see note above) or has expired. Follow the steps below to renew all certificates at the same time and for a Metro get the VPN tunnel back up.  
  
Workaround:  
  
The workaround provides the solution to each of the scenarios mentioned above.  
  
If the user forgets the CA passphrase the user has no other option than to re-create all the certificates and, in addition, to re-establishing the VPN in the case of a VPLEX-Metro configuration. Use the following steps to re-create the passphrases. **Document** the new passphrase once created.  

This article has been broken down into sections based on which VPLEX GeoSynchrony code version\* the VPLEX is running, and there is a subsequent section on cluster-witness.

  
\--------------------------------------------------------------------------------------------------------------------------------------------  
\*Note: If you are running on any GeoSynchrony code version before 6.2.x, those versions are End of Service Support (EOSS) and no longer supported. After re-creating the security certificates please make plans to upgrade your VPLEX to the latest code release to ensure you are running on the latest supported versions of code which will get you fixes, enhancements, any new features and fixed security vulnerabilities that have been made since the code you are currently running was released that you will benefit from.  
\--------------------------------------------------------------------------------------------------------------------------------------------

**!!!!!!!!!!!!!!!!!!!!!! PLEASE REVIEW THE DETAILS BELOW!!!!!!!!!!!!!!!!!!!!!!!**

  
**Table of Contents -** **jump to a specific section:**

  
[Section-A: GeoSynchrony 6.2 P5 and later; renew the certificates at the GUI](https://tools.jet.su/emc_kb/000169421/#section_A)  
[Section-B: GeoSynchrony 5.0.x and 5.1.x code levels (EOSS)](https://tools.jet.su/emc_kb/000169421/#section_B) (requires root password, must be performed by support)  
[Section-C: GeoSynchrony 5.2.x code levels (EOSS)](https://tools.jet.su/emc_kb/000169421/#section_C) (requires root password, must be performed by support)  
[Section-D: GeoSynchrony 5.3.x and 5.4.x code levels (EOSS)](https://tools.jet.su/emc_kb/000169421/#section_D)  
[Section-E: GeoSynchrony 5.5.x (EOSS) and 6.x code levels](https://tools.jet.su/emc_kb/000169421/#section_E) (6.0.x and 6.1.x are EOSS)  
[Section-F: Cluster-Witness (Metro configurations only)](https://tools.jet.su/emc_kb/000169421/#section_F)  
  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Section-A: For 6.2 P5 and later, how to renew certificates in the GUI:

If you are running GeoSynchrony 6.2 Patch 5 and higher and you received an e-mail alert letting you know that the host certificate is going to expire in x days you can do two things to renew the host and all certificates.  
  
1\. There is the option above to [Follow the steps below to renew all certificates at the same time](https://tools.jet.su/emc_kb/000169421/#section_Y) and follow the instructions listed there or, there is also the steps below to renew certificates using the GUI as follows;

1. Access the GUI and in the Dashboard > SYSTEM STATUS, at the bottom of the data you will see the health status of the cluster and the last item is the 'Certificate Status'.
2. If the certificate status is green nothing needs to be done.
3. If the certificate status shows as Yellow or Red, go to the upper right of the GUI and you will see 'Settings', click this and in the drop down list select 'Security'.
4. If the certificate status is gray, please follow the actions provided in this KBA to re-create all certificates.

Example of steps using the GUI to renew certificates at 6.2 Patch 5 and later:  
![image.png](https://tools.jet.su/emc_kb/000169421/ka06P000000oT9mQAE_en_US_2.jpeg)  

1. In the Security view are the certificates, hostCert, webServerHostCert and strongswan, this is the CA cert the other two are signed to, and the data tells the type of each certificate, who it is issued to, issued by, used by, if the date is valid and the expiry date of each.

  
![image.png](https://tools.jet.su/emc_kb/000169421/ka06P000000oT9mQAE_en_US_3.jpeg)

1. The user then either selects the certificate with the date coming up on expiration or can renew all listed certificates. The recommendation is to always renew all certificates.
1. Once the selection(s) have been made then press the RENEW button, you will need to enter the Passphrase, so have the one used previously available. If you forgot or don't have the Passphrase you will need to follow the steps in this KBA to re-create new certificates which will cover creating a new Passphrase.
1. For more details on these steps, in the upper right next to Service is the help icon ![image.png](https://tools.jet.su/emc_kb/000169421/ka06P000000oT9mQAE_en_US_4.jpeg)
1. Click on the help icon and in the drop down list select "Unispshere for VPLEX Help"

![image.png](https://tools.jet.su/emc_kb/000169421/ka06P000000oT9mQAE_en_US_5.jpeg)

1. In the initial "Welcome" help screen, in the upper right is a search field, type in "certificate" and select "renew the self-signed certificates" and in the Results screen click on "Renew the self-signed certificates" here. This will bring you to that help screen.
1. This screen provides the steps to renew the certificate(s).

\[

### Section-B: For 5.0x and 5.1x code levels (EOSS):

  
NOTE:  
If performing this procedure on a VPLEX Local then perform every step, except for Steps #1, #4, #8, #9 and ignore the comments for "both clusters"  
  
1\. In VPlexcli on both clusters (*Skip if VPLEX Local*): **vpn stop** Example:  
VPlexcli:/> **vpn stop**  
  
2\. In VPlexcli on both clusters (*required for VPLEX Local*): **security delete-ca-certificate**  
**security delete-host-certificate**  
**security delete-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**  
**security delete-ca-certificate -o webStrongswanCert.pem**

  
3\. Only Cluster-1 VPlexcli (*required for VPLEX Local*):

**security create-ca-certificate**

  
4\. Only Cluster-1 at management-server prompt (*Skip if VPLEX Local*):

**scp /etc/ipsec.d/cacerts/strongswanCert.pem service@<Cluster-2-IP>:/etc/ipsec.d/cacerts** **scp /etc/ipsec.d/private/strongswanKey.pem service@<Cluster-2-IP>:/etc/ipsec.d/private**

  
5\. On both clusters at management-server prompt (*requried for VPLEX Local*):

**sudo /usr/java/jre1.6.0\_03/bin/keytool -delete -alias ROOT -keystore /usr/java/jre1.6.0\_03/lib/security/cacerts -storetype jks -storepass changeit** **sudo /usr/java/jre1.6.0\_03/bin/keytool -importcert -file /etc/ipsec.d/cacerts/strongswanCert.pem -alias ROOT -keystore /usr/java/jre1.6.0\_03/lib/security/cacerts -storetype jks -storepass changeit -noprompt**

  
Note: If, after running the above commands, you get the message "alias vplex.root does not exist", ignore and proceed to the next step. What this message means is that the first time the passphrase was created the java keystore file was not created.  

6\. On both clusters in VPlexcli (*Required for VPLEX Local*):

**security create-host-certificate**

**security create-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**

  
7\. In this step make sure you are at the "home" prompt level of the management server, /home/service. To do this from the prompt type "cd", then to check that you are at the "home" prompt, type "pwd" and you should see "/home/service" listed,  
  
Example:

To return to the home prompt:

service@ManagementService:/var/log/VPlex/cli> **cd**  
service@ManagementService:~>

  
Then to ensure you at the home prompt:

service@ManagementService:~> **pwd**  
/home/service *<< indicates you are at the home prompt for this step*  
service@ManagementService:~ >

  
Now follow the next actions:  
On both clusters at management-server home prompt (Required for VPLEX Local):

**/opt/emc/VPlex/tools/utils/JKSsetup.pl**  
**sudo /etc/init.d/VPlexManagementConsole restart**

  
8\. Both clusters in VPlexcli, cluster-1 first, then cluster-2 (Skip if VPLEX Local):

**security ipsec-configure -i <ip address of remote management server>  
vpn start**

  
9\. On both clusters in VPlexcli (Skip if VPLEX Local):

**vpn status**

Confirm the VPN is fully established. Check that the remote management server is reachable, that IPSEC is UP, that the remote Gateway is reachable and the the Cluster Witness Server is reachable.  
  
Sample output:

VPlexcli:/> vpn status  
Verifying the VPN status between the management servers...  
IPSEC is UP <--  
Remote Management Server at IP Address 10.241.164.241 is reachable <--  
Remote Internal Gateway addresses are reachable <--  
  
Verifying the VPN status between the management server and the cluster witness server...IPSEC is UP <--  
Cluster Witness Server at IP Address 128.221.254.3 is reachable <--

If 128.221.254.3 is unreachable continue to [Section-F "Cluster-Witness Section"](https://tools.jet.su/emc_kb/000169421/#section_F), if not stop here since the procedure is finished.

  
\[\]  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Section-C: For 5.2.x code levels (EOSS):

NOTE:  
If performing this procedure on a VPLEX Local then perform every step except for Steps #1, #4, #8, #9 and ignore the comments for "both clusters"

1\. In VPlexcli on both clusters (Skip if VPLEX Local):  
  
**vpn stop**  
  
Example:  
VPlexcli:/> **vpn stop**  
  
2\. In VPlexcli on both clusters(Required for VPLEX Local):

**security delete-ca-certificate  
security delete-host-certificate  
security delete-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem  
security delete-ca-certificate -o webStrongswanCert.pem**

  
3\. Only Cluster-1 VPlexcli (Required for VPLEX Local):

**security create-ca-certificate**

  
4\. Only Cluster-1 at management-server prompt (Skip if VPLEX Local):

**scp /etc/ipsec.d/cacerts/strongswanCert.pem service@<Cluster-2-IP>:/etc/ipsec.d/cacerts  
  
scp /etc/ipsec.d/private/strongswanKey.pem service@<Cluster-2-IP>:/etc/ipsec.d/private**

  
5\. On both clusters at management-server prompt (Required for VPLEX Local):

**sudo /usr/java/jre1.6.0\_45/bin/keytool -delete -alias ROOT -keystore /usr/java/jre1.6.0\_45/lib/security/cacerts -storetype jks -storepass changeit**  
  
**sudo /usr/java/jre1.6.0\_45/bin/keytool -importcert -file /etc/ipsec.d/cacerts/strongswanCert.pem -alias ROOT -keystore /usr/java/jre1.6.0\_45/lib/security/cacerts -storetype jks -storepass changeit -noprompt**

  
  
Note: If, after running the above commands, you get the message "alias vplex.root does not exist", ignore and proceed to the next step. What this message means is that the first time the passphrase was created the java keystore file was not created.  
  
6\. On both clusters in VPlexcli (Required for VPLEX Local):

**security create-host-certificate  
security create-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**

  
7\. In this step make sure you are at the "home" prompt level of the management server, /home/service. To do this from the prompt type "cd", then to check that you are at the "home" prompt, type "pwd" and you should see "/home/service" listed,  
  
Example:

To return to the home prompt:

service@ManagementService:/var/log/VPlex/cli> **cd**  
service@ManagementService:~>

  
Then to ensure you at the home prompt:

service@ManagementService:~> **pwd**  
/home/service *<< indicates you are at the home prompt for this ste* p  
service@ManagementService:~>

  
Now follow the next actions:  
On both clusters at management-server home prompt (Required for VPLEX Local):

**/opt/emc/VPlex/tools/utils/JKSsetup.pl  
sudo /etc/init.d/VPlexManagementConsole restart**

  
  
8\. Both clusters in VPlexcli, cluster-1 first, then cluster-2 (Skip if VPLEX Local):

**security ipsec-configure -i <ip address of remote management server>  
vpn start**

  
9\. On both clusters in VPlexcli (Skip if VPLEX Local):

**vpn status**

  
Confirm the VPN is fully established. Check that the remote management server is reachable, that IPSEC is UP, that the remote Gateway is reachable and the the Cluster Witness Server is reachable.  
  
Sample output:  
VPlexcli:/> vpn status  
Verifying the VPN status between the management servers...  
IPSEC is UP <--  
Remote Management Server at IP Address 10.241.164.241 is reachable <--  
Remote Internal Gateway addresses are reachable <--  
  
Verifying the VPN status between the management server and the cluster witness server...  
IPSEC is UP <--  
Cluster Witness Server at IP Address 128.221.254.3 is reachable <--  
  
If 128.221.254.3 is unreachable continue to [Section-F "Cluster-Witness Section"](https://tools.jet.su/emc_kb/000169421/#section_F), if not stop here since the procedure is finished.

  
\[\]  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Section-D: For 5.3.x and 5.4.x code levels (EOSS):

NOTE:  
If performing this procedure on a VPLEX Local then perform every step except for Steps #1, #4, #8, #9 and ignore the comments for "both clusters"

1\. In VPlexcli on both clusters (Skip if VPLEX Local):  
  
**vpn stop**  
  
Example:  
VPlexcli:/> **vpn stop**  
  
2\. In VPlexcli on both clusters (Required for VPLEX Local):

**security delete-ca-certificate  
security delete-host-certificate  
security delete-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**  
**security delete-ca-certificate -o webStrongswanCert.pem**

  
3\. Only Cluster-1 VPlexcli (Required for VPLEX Local):

**security create-ca-certificate**

  
4\. Only Cluster-1 at management-server prompt (Skip if VPLEX Local):

**scp /etc/ipsec.d/cacerts/strongswanCert.pem service@<Cluster-2-IP>:/etc/ipsec.d/cacerts  
  
scp /etc/ipsec.d/private/strongswanKey.pem service@<Cluster-2-IP>:/etc/ipsec.d/private**

  
5\. On both clusters at management-server prompt (Required for VPLEX Local):

**sudo /usr/java/default/bin/keytool -delete -alias vplex.root -keystore /var/log/VPlex/cli/default.cacerts -storetype jks -storepass changeit  
  
sudo /usr/java/default/bin/keytool -importcert -file /etc/ipsec.d/cacerts/strongswanCert.pem -alias vplex.root -keystore /var/log/VPlex/cli/default.cacerts -storetype jks -storepass changeit -noprompt**

  
Note: If, after running the above commands, you get the message "alias vplex.root does not exist", ignore and proceed to the next step. What this message means is that the first time the passphrase was created the java keystore file was not created.  
  
6\. On both clusters in VPlexcli (Required for VPLEX Local):

**security create-host-certificate  
security create-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**

  
7\. In this step make sure you are at the "home" prompt level of the management server, /home/service. To do this from the prompt type "cd", then to check that you are at the "home" prompt, type "pwd" and you should see "/home/service" listed,  
  
Example:

To return to the home prompt:

service@ManagementService:/var/log/VPlex/cli> **cd**  
service@ManagementService:~>

  
Then to ensure you at the home prompt:

service@ManagementService:~> **pwd**  
/home/service << indicates you are at the home prompt for this step  
service@ManagementService:~>

  
Now follow the next actions:  
On both clusters at management-server home prompt (Required for VPLEX Local):

**/opt/emc/VPlex/tools/utils/JKSsetup.pl  
sudo /etc/init.d/VPlexManagementConsole restart**

  
  
8\. Both clusters in VPlexcli, cluster-1 first, then cluster-2 (Skip if VPLEX Local):

**security ipsec-configure -i <ip address of remote management server>  
vpn start**

  
9\. On both clusters in VPlexcli (Skip if VPLEX Local):

**vpn status**

  
Confirm the VPN is fully established. Check that the remote management server is reachable, that IPSEC is UP, that the remote Gateway is reachable and the the Cluster Witness Server is reachable.  
  
Sample output:  
VPlexcli:/> vpn status  
Verifying the VPN status between the management servers...  
IPSEC is UP <--  
Remote Management Server at IP Address 10.241.164.241 is reachable <--  
Remote Internal Gateway addresses are reachable <--  
  
Verifying the VPN status between the management server and the cluster witness server...  
IPSEC is UP <--  
Cluster Witness Server at IP Address 128.221.254.3 is reachable <--  
  
If 128.221.254.3 is unreachable continue to [Section-F "Cluster-Witness Section"](https://tools.jet.su/emc_kb/000169421/#section_F), if not stop here since the procedure is finished.  
  
\[\]

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Section-E: For 5.5.x (EOSS) and 6.x code levels (6.0.x and 6.1.x are EOSS):

NOTE:  
If performing this procedure on a VPLEX Local then perform every step except for Steps #1, #4, #5 and ignore the comments for "both clusters"

1\. In VPlexcli on both clusters (Skip if VPLEX Local):  
  
**vpn stop**  
  
Example:  
VPlexcli:/> **vpn stop**  
  
2\. In VPlexcli on both clusters (Required for VPLEX Local):  
  
**security delete-ca-certificate  
security delete-host-certificate  
security delete-host-certificate -o webServerHostCertFile.pem -f webServerHostkeyFile.pem**  
**security delete-ca-certificate -o webStrongswanCert.pem**

  
3\. Both clusters in VPlexcli, cluster-1 first ( (Required for VPLEX Local), then cluster-2  
  
**security configure-certificates**

Note: If you run this command and receive an error about certificates already exist, please 'exit' to the management-server prompt and remove the old stale certificates with the command as follows, then re-try step #3:  
  
**rm /etc/ipsec.d/\*/\*pem\***

4\. Both clusters in VPlexcli, cluster-1 first, then cluster-2 (Skip if VPLEX Local):  
  
**security ipsec-configure -i <ip address of remote management server>  
vpn start**  
  
5\. On both clusters in VPlexcli (Skip if VPLEX Local):  
  
**vpn status**  
  
Confirm the VPN is fully established. Check that the remote management server is reachable, that IPSEC is UP, that the remote Gateway is reachable and the the Cluster Witness Server is reachable.  
  
Sample output:  
VPlexcli:/> vpn status  
Verifying the VPN status between the management servers...  
IPSEC is UP <--  
Remote Management Server at IP Address 10.241.164.241 is reachable <--  
Remote Internal Gateway addresses are reachable <--  
  
Verifying the VPN status between the management server and the cluster witness server...  
IPSEC is UP <--  
Cluster Witness Server at IP Address 128.221.254.3 is reachable <--  
  
If 128.221.254.3 is unreachable continue to [Section-F "Cluster-Witness Section"](https://tools.jet.su/emc_kb/000169421/#section_F), if not stop here since the procedure is finished.  
  
\[\]

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Section-F: Cluster Witness (If Cluster-Witness is deployed, VPLEX Metro/Geo only)

NOTE:  
This section below should only be performed on VPLEX Metro configurations in which Cluster-Witness has been installed/configured.

1\. To find the public IP of cluster-witness run the following VPlexcli command:  
  
VPlexcli:/> **ll /cluster-witness/**  
  
Sample Output:

/cluster-witness:  
  
Attributes:  
Name Value  
\------------------ -------------  
admin-state unknown  
private-ip-address 128.221.254.3  
public-ip-address XX.XX.XX.XX *<<< Cluster-Witness public IP*

  
2\. SSH to the public IP of cluster-witness  
  
service@ManagementServer:~> **ssh <cluster-witness-public-IP>**  
  
Sample output:  
service@ManagementServer:~> ssh xx.xx.xx.xx  
Warning: Permanently added 'xx.xx.xx.xx' (ECDSA) to the list of known hosts.  
Last login: Mon Jun 06 15:33:14 2016 from xx.xx.xx.xx  
service@ClusterWitness:~>  
  
3\. Check the hostkey passphrase of cluster-witness  
The cluster-witness hostkey passphrase may be different than the management-servers. Please check with the following command:  
  
service@cluster-witness:~> **tail -1 /etc/ipsec.secrets**  
  
Sample output:  
service@cluster-witness:~> **tail -1 /etc/ipsec.secrets**  
: RSA hostKey.pem strongswan *<--The passphrase in this example is strongswan*  
  
Keep note of this value as you will need it when running step-5. If the passphrase is between " " don't include them.  
  
4\. Remove the four certificate files on the cluster-witness server, as follows:  
  
service@cluster-witness:~> **rm /etc/ipsec.d/\*/\*pem**  
  
Note: If you first want to see all the \*pem files you are about to remove, run the command  
**ll /etc/ipsec.d/\*/\*pem**  
  
Sample output:

service@ClusterWitness:~> ll /etc/ipsec.d/\*/\*pem  
\-rw-r--r-- 1 service users 1655 Mar 1 05:49 /etc/ipsec.d/cacerts /strongswanCert.pem  
\-rw-r--r-- 1 service users 4620 Mar 1 05:49 /etc/ipsec.d/certs/hostCert.pem  
\-rw-r--r-- 1 service users 1751 Mar 1 05:49 /etc/ipsec.d/private/hostKey.pem  
\-rw-r--r-- 1 service users 1743 Mar 1 05:49 /etc/ipsec.d/private/strongswanKey.pem  

5\. Run the following VPlexcli command on both clusters:  
  
First from VPlexcli in Cluster-1  
VPlexcli:/> **configuration cw-vpn-configure -i cluster-witness-public-IP --force**  
  
Then from VPlexcli in Cluster-2  
VPlexcli:/> **configuration cw-vpn-configure -i cluster-witness-public-IP --force**  
  
\*Note: Make sure to be aware of the prompts for passphrases. You will be asked for the management-server passphrase as well as the cluster-witness passphrase. These may be different. Entering the incorrect values may lead to VPN not establishing  
  
6\. Run vpn status on both clusters and confirm the VPN is fully established. Check that the remote management server is reachable, that IPSEC is UP, that the remote Gateway is reachable and the the Cluster Witness Server is reachable.  
  
Sample output:

VPlexcli:/> vpn status  
Verifying the VPN status between the management servers...  
IPSEC is UP <--  
Remote Management Server at IP Address xx.xx.xx.xxis reachable <--  
Remote Internal Gateway addresses are reachable <--

  
7\. Verifying the VPN status between the management server and the cluster witness server.

IPSEC is UP <--  
Cluster Witness Server at IP Address 128.221.254.3 is reachable <--

  
8\. Run the following VPlexcli command on both clusters:  
  
**ll cluster-witness**  
  
Sample output:

VPlexcli:/> ll cluster-witness  
/cluster-witness:  
  
Attributes:  
Name Value  
\------------------ -------------  
admin-state disabled <--  
private-ip-address 128.221.254.3  
public-ip-address XX.XX.XX.XX <--  
  
Contexts:  
Name Description  
\---------- --------------------------  
components Cluster Witness Components

  
9\. Enable and verify the cluster witness by running the following cli commands on Both  
Clusters:  
  
VPlexcli:/> **cluster-witness enable**  
VPlexcli:/> **ll cluster-witness**  
  
\[\]

###### Additional Information

If, after following the steps above and you run ' **vpn status** ' and the VPN is still not established, contact Dell Customer Support and mention this article number.  

**NOTE:** Currently the Video KBA below is not up-to-date with this KBA. We are working to get the Video KBA updated. **For now, it is not recommended to view the Video as it does have out-of-date information at this time.**  
  
![](https://www.youtube.com/watch?v=RgM9bOuoXuU)

###### Partner Notes

**Notes:**  
1\] If after following the steps in this article, and the user ran ' **vpn status** ' to confirm the connectivity between  
the two clusters and the cluster-witness, if configured, and gets unreachable at the Cluster-Witness private IP,  
128.221.254.3, refer to article 000105530, [VPLEX: Cannot reset cluster witness VPN configuration](https://tools.jet.su/emc_kb/000105530/index.html).  
  
2\] If you receive the "error: ss1.pem: Permission Denied", you may have used the wrong passphrase.  
To check the passphrase run the following command from the management server  
  
(NOTE:that you will need to do this from both management servers if it is a VPLEX-Metro):

**cat /etc/ipsec.secrets**

EXAMPLE:  
service@ManagementServer:~> **cat /etc/ipsec.secrets**  
#  
\# ipsec.secrets  
#  
\# This file holds the RSA private keys or the PSK preshared secrets for  
\# the IKE/IPsec authentication. See the ipsec.secrets(5) manual page.  
#  
: RSA hostKey.pem **strongswan** <--The passphrase in this example is strongswan

  
3\] If you find the passphrase was different than what you expected, "vi" the 'ipsec.secrets' file and change the  
passphrase to what you expect it to be. If you are not comfortable with "vi", please engage the VPLEX  
support lab to have this file changed. Once this is complete, start this KB article over from Step 1.

###### Internal Notes

**Note:**  
For additional information, see ClearQuest defects [UZEPH00014279](https://confluence.cec.lab.emc.com/display/CSE/zeph-q14279), and [UZEPH00023878.](https://confluence.cec.lab.emc.com/display/CSE/zeph-q23878)  
For additional information on GeoSynchrony 5.3 entries, see ClearQuest defect [UZEPH00029697](https://confluence.cec.lab.emc.com/display/CSE/zeph-q29697).  
ClearQuest access is only available to authorized Customer Service Representatives.

#### Article Properties

---

###### Affected Product

VPLEX for All Flash, VPLEX Series, VPLEX VS2, VPLEX VS6

###### Last Published Date

15 May 2023

###### Version

8

###### Article Type

Solution