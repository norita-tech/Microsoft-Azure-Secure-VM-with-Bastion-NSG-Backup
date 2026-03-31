# Azure Secure VM Deployment with Bastion, NSG & Backup
## Overview
This project demonstrates how to securely deploy a Windows virtual machine in Azure without a public IP, using:

Virtual Network + Subnet

Network Security Group (NSG)

Azure Bastion for secure RDP access

Azure Backup for VM protection

This setup follows real‑world security best practices by eliminating public exposure and enforcing controlled access through Bastion.


Architecture
Text‑Based Diagram
Azure Secure VM Architecture

+---------------------------------------------------------------+
|                        Resource Group                         |
|                    rg-secure-vm-demo                          |
+---------------------------------------------------------------+

+----------------------+        +------------------------------+
|   Virtual Network    |        |   Network Security Group     |
|   vnet-secure-demo   |        |       nsg-app-subnet         |
|   10.0.0.0/16        |        |   Inbound: Allow RDP (100)   |
+----------+-----------+        +------------------------------+
           |
           | Subnet: subnet-app (10.0.1.0/24)
           v
+---------------------------------------------------------------+
|                     Virtual Machine                           |
|                       vm-secure-app                           |
|                 Windows Server 2022/2025                      |
|                 Public IP: None                               |
+---------------------------------------------------------------+

+---------------------------------------------------------------+
|                         Azure Bastion                         |
|                 Secure browser-based RDP access               |
+---------------------------------------------------------------+

+---------------------------------------------------------------+
|                 Recovery Services Vault (Backup)              |
|                 Daily backup using default policy             |
+---------------------------------------------------------------+

A. Create Resource Group
Steps
Azure Portal → Resource groups

Create

Name: rg-secure-vm-demo

Region: West Europe (or your chosen region)

Review + create → Create

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 B. Create VNet + Subnet
Steps
Azure Portal → Virtual networks

Create

Name: vnet-secure-demo

Address space: 10.0.0.0/16

Add subnet:

Name: subnet-app

Range: 10.0.1.0/24

Review + create → Create

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 C. Create NSG + Associate
Steps
Azure Portal → Network security groups

Create

Name: nsg-app-subnet

After creation → Subnets → Associate

Select:

VNet: vnet-secure-demo

Subnet: subnet-app

Add inbound rule:
Service: RDP

Priority: 100

Action: Allow

Source: Any

Protocol: TCP (correct for RDP)

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 D. Create VM (No Public IP)
Steps
Azure Portal → Virtual machines → Create

Name: vm-secure-app

Image: Windows Server 2022/2025

Authentication: Password

Networking tab:

VNet: vnet-secure-demo

Subnet: subnet-app

Public IP: None

NIC NSG: None (subnet NSG already applied)

Review + create → Create

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 E. Deploy Bastion
Steps
Open the VM → Connect → Bastion

Click Deploy Bastion

Accept defaults

Review + create → Create

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 F. Connect via Bastion
Steps
VM → Connect → Bastion

Enter VM credentials

Browser RDP session opens

📸 Screenshot
[Looks like the result wasn't safe to show. Let's switch things up and try something else!]

🧩 G. Enable Backup
Steps
VM → Backup

Create new Recovery Services Vault

Apply Default policy

Enable backup

![Backup ](screenshots-vm-secure/backup-config.png)

🎯 Skills Demonstrated
Secure VM deployment (no public IP)

Azure Bastion configuration

Network Security Groups (NSG)

Virtual Networks & Subnets

Azure Backup configuration

Identity & access isolation

Cloud security best practices

Professional documentation & architecture design

🏁 Conclusion
This project demonstrates how to deploy a secure Azure VM using best practices:

No public exposure

Controlled access via Bastion

Network segmentation

Backup protection





