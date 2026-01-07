# Lab 01 – Active Directory Domain Controller (AD DS)

## 🎯 Goal
Set up a Windows Server as a Domain Controller and join a Windows client to the domain.

## 🧰 Environment
- Hyper-V / VMware
- Windows Server 2022 (DC01)
- Windows 10/11 Client (CL01)
- Network: NAT or Internal vSwitch

## ✅ Prerequisites
- Server installed and updated
- Static IP configured on DC01
- Administrator access on both machines

---

## Step 1 – Set a static IP on DC01
1. Open: Network Settings → Adapter → IPv4
2. Configure:
   - IP: 192.168.10.10
   - Mask: 255.255.255.0
   - Gateway: 192.168.10.1
   - DNS: 192.168.10.10

📸 Screenshot: `images/lab01-static-ip.png`

---

## Step 2 – Rename server and restart
Rename server to: `DC01`  
Restart the server.

PowerShell (optional):
```powershell
Rename-Computer -NewName "DC01" -Restart


##### Step 3 – Install AD DS role

Server Manager → Add Roles and Features

Select:

Active Directory Domain Services

Add required features

PowerShell (optional):

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools


📸 Screenshot: images/lab01-adds-role.png

###### Step 4 – Promote to Domain Controller

Server Manager → Notification flag → Promote this server to a domain controller

Choose: Add a new forest

Domain name example: lab.local

Set DSRM password

Install and restart

PowerShell (optional):

Install-ADDSForest -DomainName "lab.local" -InstallDNS


📸 Screenshot: images/lab01-promote-dc.png

###### Step 5 – Verify AD & DNS

Check:

AD Users and Computers

DNS Manager

Event Viewer (Directory Service / DNS)

📸 Screenshot: images/lab01-aduc.png

###### Step 6 – Join client (CL01) to the domain

On the client:

Set DNS = 192.168.10.10

System → Rename this PC (advanced) → Domain: lab.local

Use domain admin credentials

Restart

📸 Screenshot: images/lab01-join-domain.png

###### ✅ Result

Domain Controller is running

DNS installed

Client successfully joined the domain

🧩 Notes / Issues

(Write any problems you faced and how you fixed them)


---

##### 
