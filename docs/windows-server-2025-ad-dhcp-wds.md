# Windows Server 2025 -AD, DNS, DHCP Failover & WDS  


This lab is a continuation of the basic Active Directory lab.  
It builds upon the existing domain infrastructure by adding high availability networking services and automated deployment  

Previos lab:  
- Windows Server 2025 - Active Directory Basics

## Goal
The goal of this lab is to extend an existing Active Directory enviroment with enterprise-level services such as DHCP Failover and Windows Deployment  Services (WDS)  

## Envuronment
- Existing AD Domain: lab.local
- DC01: Primary Domain Controller, DNs, DHCP, WDS
- DC02: Additional Domain Controller, DNS, DHCP Failover partner
- Hyper-V virtualized environment
- Windows 10 PXE Client

## Implemented Components  
### Active Directory Exension
- Added a second domain controller (DC02)
- Verified AD replication between DC01 and DC02
![DC02 Computer Rename](../images/ad-dhcp-failover-wds/ws2025-dc02-rename.png)
![DC02 Joined Domain](../images/ad-dhcp-failover-wds/ws2025-dc02-domain-joined.png)
![Install AD DS on DC02](../images/ad-dhcp-failover-wds/ws2025-dc02-install-adds.png)
![Promote DC02 to Domain Controller](../images/ad-dhcp-failover-wds/ws2025-dc02-promote-existing-domain.png)
![DC02 Promoted Successfully](../images/ad-dhcp-failover-wds/ws2025-dc02-promoted.png)

### DNS
- Active Directory-integrated DNS
- Verified forward and reverse name resolution
![DC02 Domain Controller Options](../images/ad-dhcp-failover-wds/ws2025-dc02-dc-options.png)
![AD Replication Successful](../images/ad-dhcp-failover-wds/ws2025-dc02-replication-ok.png)


### DHCP with Failover
- Configured IPv4 scope (192.168.10.0/24)
- Implemented DHCP Failover between DC01 and DC02
- Tested lease replication and failover behavior
![Install DHCP Server](../images/ad-dhcp-failover-wds/ws2025-install-dhcp.png)
![DHCP Authorized in Active Directory](../images/ad-dhcp-failover-wds/ws2025-dhcp-authorized.png)
![DHCP Server IP Configuration](../images/ad-dhcp-failover-wds/ws2025-dhcp-ip.png)
![DHCP Scope Range](../images/ad-dhcp-failover-wds/ws2025-dhcp-scope-range.png)
![DHCP Gateway Not Configured](../images/ad-dhcp-failover-wds/ws2025-dhcp-gateway-empty.png)
![DHCP DNS Options](../images/ad-dhcp-failover-wds/ws2025-dhcp-dns-options.png)
![DHCP Scope Active](../images/ad-dhcp-failover-wds/ws2025-dhcp-scope-active.png)
![DHCP Failover Configured](../images/ad-dhcp-failover-wds/dhcp-failover-configured.png)
![DHCP Installed on DC02](../images/ad-dhcp-failover-wds/dhcp-dc02-installed.png)

### Windows Deployment Services (WDS)
- Installed WDS in AD-integrated mode
![WDS Installed on DC01](../images/ad-dhcp-failover-wds/wds-installed-dc01.png)
![WDS Initial Configuration Successful](../images/ad-dhcp-failover-wds/wds-initial-config-ok.png)

- Added Windows PE boot image
![WDS Boot Image Added](../images/ad-dhcp-failover-wds/wds-boot-image-added.png)

- Added Windows install image
![WDS Install Image Added](../images/ad-dhcp-failover-wds/wds-install-image-added.png)

- Configured PXE response settings
### PXE Boot Verification
- Successfully booted a Hyper-v client via PXE
- Client loaded Windows PE and reached Windows Setup
![PXE Boot Windows Setup](../images/ad-dhcp-failover-wds/wds-pxe-windows-setup-ok.png)


## Result  
This lab demonstrates a scalable and highly available Windows Server infrastructure built on top of an existing Active Directory domain.
