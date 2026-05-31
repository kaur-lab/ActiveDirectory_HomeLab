<h1 id="top"> Active Directory Lab Setup Guide (VirtualBox) </h1>
This step-by-step guide will walk you through building your own Active Directory lab from scratch using VirtualBox. You'll create two virtual machines: a Domain Controller (Windows Server 2019) and a Client Machine (Windows 10 Pro), configure them, join the domain, and get everything set up for hands-on Active Directory tasks.
---
## <h2 id="table-of-contents"> 🗂️ Table of Contents </h2>

- [⚙️ VirtualMachine Installation](#vm-installation)
- [Domain Controller (DC01)](#domain-controller-dc01)
  - [🛠️ Virtual Machine Setup](#virtual-machine-setup-dc01)
  - [💽 Windows OS Installation](#windows-os-installation-dc01)
  - [🌐 Network and AD Configuration](#network-and-ad-configuration-dc01)
- [Client Machine (CLIENT01)](#client-machine-client01)
  - [🛠️ Virtual Machine Setup](#virtual-machine-setup-client01)
  - [💽 Windows OS Installation](#windows-os-installation-client01)
  - [🌐 Network Configuration](#network-configuration-client01)
  - [🧑‍💻 Join CLIENT01 to the Domain](#join-client01-to-the-domain)

---

## <h2 id="vm-installation"> ⚙️ VirtualMachine Installation </h2>

1. Download Virtual Mchine (https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html) from the official Oracle site.
2. Right click and run the installer as administrator.
3. Leave the default installation settings unless you have specific reason to change them.
4. Complete the installation and reboot if prompted.
5. Run Virtual Machine normally. 
