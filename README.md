# 🎯 GOAD (Game of Active Directory) - Bare-Metal Deployment & Kill Chain

[![Medium](https://img.shields.io/badge/Medium-Read_Article-black?logo=medium)](https://medium.com/@mariomarzia007/building-an-enterprise-active-directory-cyber-range-goad-on-a-repurposed-3-node-proxmox-cluster-9adf44de2848)
[![YouTube](https://img.shields.io/badge/YouTube-Watch_Demo-red?logo=youtube)](https://youtu.be/dHV7ubUkCEw?si=dRTr3WHrtKAJmqLV)
[![PDF](https://img.shields.io/badge/PDF-Technical_Report-blue?logo=adobeacrobatreader)](GOAD_progetto.pdf)

## 📌 Project Overview
This repository contains the documentation, technical report, and video demonstration of a complete Enterprise Cyber Range deployment and Active Directory penetration test. 

Unlike standard local deployments, this GOAD environment was built from scratch on a **repurposed 3-node Proxmox bare-metal cluster**. It utilizes Proxmox SDN (VXLAN) to bridge the vulnerable Windows machines across the physical servers, completely isolated behind a custom pfSense gateway.

## 🔗 Resources
**[Step-by-Step Tutorial on Medium](https://medium.com/@mariomarzia007/building-an-enterprise-active-directory-cyber-range-goad-on-a-repurposed-3-node-proxmox-cluster-9adf44de2848)**: Learn how to build this infrastructure using Terraform, Packer, and Ansible, including solutions for VXLAN MTU fragmentation and pfSense firewalling.

**[Kill Chain Demonstration on YouTube](https://youtu.be/dHV7ubUkCEw?si=dRTr3WHrtKAJmqLV)**: Watch the execution of the full attack path, from initial access to total forest compromise.

**[Technical Report (PDF)](GOAD_progetto.pdf)**: Download the detailed Italian technical report (`GOAD_progetto.pdf`) included in this repository.

## ⚔️ Attack Path & Techniques Demonstrated
The offensive phase of this project covers a full Active Directory Kill Chain, mapped to real-world Advanced Persistent Threat (APT) behaviors:

**Reconnaissance:** Enumerating SMB shares and identifying Domain Controllers vs. Member Servers using `NetExec` based on SMB Signing status.

**Initial Access (LLMNR Poisoning):** Intercepting broadcast name resolution requests with `Responder` to capture NTLMv2 hashes.

**Credential Cracking:** Performing offline dictionary attacks using `Hashcat` to crack the captured NetNTLMv2 hashes.

**Enumeration & Lateral Movement:** Utilizing `BloodHound` to analyze AD ACLs and discover a hidden "Shortest Path" to Domain Admin via local administrator privileges.

**Domain Dominance (Golden Ticket):** Dumping the `NTDS.dit` remotely, extracting the `krbtgt` hash, and forging a Golden Ticket for persistence.

**Forest Escalation:** Exploiting Trust relationships and bypassing boundaries via **SID History Injection**, forging a ticket with Enterprise Admin privileges (-519).

**Total Compromise:** Uploading and executing `Mimikatz` as SYSTEM to perform a DCSync attack on the root domain controller, extracting the ultimate root `krbtgt` hash.

## 🛠️ Tools Used
* **Infrastructure:** Proxmox VE, pfSense, WireGuard, Terraform, Packer, Ansible
* **Offensive Security:** NetExec, Responder, Hashcat, BloodHound, Impacket (secretsdump, ticketer, lookupsid, psexec, smbclient), Mimikatz

---
*Author: Mario Marzia*
