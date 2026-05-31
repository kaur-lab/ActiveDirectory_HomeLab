<h1 id="top"> Active Directory Lab Setup Guide (VirtualBox) </h1>
This step-by-step guide will walk you through building your own Active Directory lab from scratch using VirtualBox. You'll create two virtual machines: a Domain Controller (Windows Server 2019) and a Client Machine (Windows 10 Pro), configure them, join the domain, and get everything set up for hands-on Active Directory tasks.
---
##<h2 id="table-of-contents"> 🗂️ Table of Contents </h2>

- [VirtualMachine Installation](#vm-installation)
- [Domain Controller (DC01)](#domain-controller)
  - [🛠️ Virtual Machine Setup](#virtual-machine-setup)
  - [💽 Windows OS Installation](#windows-os-installation)
  - [🌐 Network and AD Configuration](#network-and-ad-configuration)
  - [🌐 RAS/NAT Configuration](#ras-nat-configuration)
  - [🌐 DHCP Configuration](#dhcp-configuration)
- [Client Machine (CLIENT01)](#client-machine-client01)
  - [🛠️ Virtual Machine Setup](#virtual-machine-setup-client01)
  - [💽 Windows OS Installation](#windows-os-installation-client01)
  - [🌐 Network Configuration](#network-configuration-client01)
  - [🧑‍💻 Join CLIENT01 to the Domain](#join-client01-to-the-domain)


## <h2 id="vm-installation"> ⚙️ Virtual Machine Installation </h2>

1. Download Virtual Machine (https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html) from the official Oracle site.
2. Right click and run the installer as administrator.
3. Leave the default installation settings unless you have specific reason to change them.
4. Complete the installation and reboot if prompted.
5. Run Virtual Machine normally. 
---

## <h2 id="domain-controller"> ⚙️Creating Domain Controller (DC) </h2>

## <h2 id="virtual-machine-setup"> 🛠️ Virtual Machine Setup </h2>

## 1. Create the Virtual Machine (VM)
- Open **Virtual Machine**.
- Select **Create a New Virtual Machine**
  - Name the virtual machine **DC**, choose the location.
- Choose **OS: Microsoft Windows** → **Version: Windows Server 2019**.
![Name and Location](images/lab-setup/01-vm-setup.jpg)
- Hardware Customization: 
**Base Memory**: 2048 MB (2GB) recommended, but the default may work fine depending on your system.
- **Number of CPUs**: 2
<img src="images/lab-setup/02-vm-setup.png" alt="RAM and CPU" >
-Create a Virtual Hard Disk:
 **Hard Disk Type**: Virtual Disk Image
<img src="images/lab-setup/03-vm-setup.png" alt="Virtual Disk Image" >

- **Network Adapters**:
  - Leave the default NAT adapter.
  - Click 'Add'.
 
<img src="images/lab-setup/04-vm-setup.png" alt="Add Adapter" >

  - Under **Adapter 2** tab, select **Internal Network**
<img src="images/lab-setup/05-vm-setup.png" alt="Add Adapter" >
- Click 'Okay'

  **We have just created our first virtual machine! 🎉**

[🔝 Back to Top](#top)

---

## <h2 id="windows-os-installation"> 💽 Windows OS Installation </h2>

### Installing Windows Server 2019
- Power on **DC**.
- When prompted to **Press any key to boot from CD or DVD**, press any key. 
  - If you see the screen babbling about EFI, just restart the VM and maybe pay attention next time.
- Choose **Window Server 2019 Standard (Desktop Experience)**, then click 'Next'

![Standard (Desktop Experience)](images/lab-setup/06-server-setup.png)

- Accept the license terms, click `Next`.
- Choose **Custom: Install Windows only (advanced)**.

![Custom Install](images/lab-setup/07-server-setup.png)

- Select drive and click `Next`.

![Select Drive](images/lab-setup/08-server-setup.png)

- Now, it will take some time to install the window.
![Installation](images/lab-setup/09-server-setup.png)

- Set a strong local administrator password, then click 'Finish'.

![Create Local Admin](images/lab-setup/10-server-setup.png)

- Once installed, log in.
  - Click `Send Ctrl+Alt+Del to this virtual machine`.
  - Log in.
 
- Install Guest Additions CD images.
  - This improves performance, mouse behavior, and screen resolution.
  - Go to **Devices** and click Install Guest Additions CD images.
![Install VMware Tools](images/lab-setup/11-server-setup.png)
  - Now, run the **VBoxWindowsAdditions-amd64** from D: drive
  [Additions Tools Typical Install](images/lab-setup/12-server-setup.png)

  - Click `Install`, then `Finish`.
  - Click `Yes` to restart.
    - There's a mandatory restart coming up in a few steps after you rename this computer, so you can hold off on restarting if you want to. Or can you...?

**OS: Installed.**

[🔝 Back to Top](#top)
---

## <h2 id="network-and-ad-configuration"> 🌐 Network & AD Configuration </h2>
### 1. Set Static IP on DC01 (Host-Only Adapter)
- **Control Panel** → **Network and Internet** → **Network and Sharing Center** → **Change adapter settings**.

![Change Adapter Settings](images/lab-setup/14-network-setup.png)

- Right-click **X_Internal_X** and click `Properties`.

![Ethernet1 Properties](images/lab-setup/15-network-setup.png)

- Select **Internet Protocol Version 4**, then click `Properties`.

![IPv4 Properties](images/lab-setup/15.1-network-setup.png)

- Use the following:
  - IP: `172.16.0.1`
  - Subnet: `255.255.255.0`
  - Gateway: (leave blank)
  - DNS: `127.0.0.1`
- Click `OK`.
 
[🔝 Back to Top](#top
---

### 2. Rename PC
- Easiest way is, right click the start menu and go to system. Then, we will click the **rename this pc**

![Computer Name](images/lab-setup/16-network-setup.png)

- Set Computer name to `DC` Click `Next`.
![Rename Computer](images/lab-setup/17-network-setup.png)
- Click `OK` again.
- Click `Close`.
- Click `Restart Now`

[🔝 Back to Top](#top)
---
### 3. Install Active Directory Domain Services (AD DS)
- Log in (obviously).
- **Server Manager** → **Manage** → **Add Roles and Features**.

![Add Roles and Features](images/lab-setup/18-add-ad.png)

- Click through defaults until **Server Roles**.
- Check **Active Directory Domain Services**. 

![Check AD DS](images/lab-setup/19-add-ad.png)

- Click `Add Features`.

![Add Features](images/lab-setup/20-add-ad.png)

- Click through remaining prompts and click `Install`. 
  - **DO NOT CLOSE THE WINDOW!**

![Install](images/lab-setup/21-add-ad.png)


[🔝 Back to Top](#top)

---
### 4. Promote DC to Domain Controller
- Select **Promote this server**.

![Promote Server](images/lab-setup/22-add-ad.png)

- And for those of you didn't pay attention to the warning about closing the window, you'll see a yellow notification like this on your Server Manager Dashboard. Click on it.
- Click **Promote this server to a domain controller**.
- Select **Add a new forest**.
- Set the Root domain name to `mydomain.com`.

![Domain Name](images/lab-setup/23-add-ad.png)

- Set DSRM password.
  - Write it down as we'll need it for certain recovery tasks.
- Click `Next`.

![Set DSRM Password](images/lab-setup/26-add-ad.png)

- Accept defaults in the following sections and click `Install`.
  - The yellow warnings are ok. As long as there are no actual errors you'll be fine. Trust me...

![Install Forest](images/lab-setup/24-add-ad.png)

- Server will reboot automatically after configuration.

![Reboot](images/lab-setup/25-add-ad.png)

**We’ve just created our own domain controller! 🎉**
---

## <h2 id="ras-nat-configuration"> 🌐 RAS/NAT Configuration </h2>

This will allow the client to access the internet even though when its on private virtual network.
- Click **Add roles and features**.

![Add Roles and Features](images/lab-setup/18-add-ad.png)

- Click through defaults until **Server Roles**.
- Check **Remote Access**.
   
![Check AD DS](images/lab-setup/30-ras-nat.png)

- Click through default until **Role Service**.
- Check **Routing**
  
![Add Service](images/lab-setup/31-ras-nat.png)

- Click through remaining prompts and click `Install`.
  
![Standard)](images/lab-setup/32-ras-nat.png)

- Now, choose **Tools** right top corner.
  
![Standard)](images/lab-setup/35-ras-nat.png)

-Right click **DC (local)** and choose 'Configure and Enable Routing and Remote Access'

![Standard)](images/lab-setup/33-ras-nat.png)

-Now start the installation an choose **Network Address Translation (NAT)** in configuration window

![Standard)](images/lab-setup/34-ras-nat.png)

- On next window, you will see our two IP addresses that we configured earlier.
   - Choose the internet one
     
![Standard)](images/lab-setup/36-ras-nat.png)

- Click 'Next' and then 'Finish'
- This is finished. Now, when the client window is setup they will be able to get to internet
  
![Standard)](images/lab-setup/37-ras-nat.png)

[🔝 Back to Top](#top)

---

## <h2 id="dhcp-configuration"> 🌐 DHCP Configuration </h2>
DHCP will allow all client computers on network to automatically get their IP addresses.
We will follow same steps that we used for installing AD DS, except this time we choose DHCP Server
- Click **Add roles and features*

 ![Add Roles and Features](images/lab-setup/18-add-ad.png)

- Click through defaults until **Server Roles**.
- Check **DHCP Server**.
  
![Check AD DS](images/lab-setup/38-dhcp.png)

- CLick **Add roles** and keep on choosing default until 'Install'
  
![Check AD DS](images/lab-setup/39-dhcp.png)

Our DHCP Server is installed.
###  Now we could setup the scope for our DHCP Server
Now we will define scope, means, the IP address range from which DHCP will automatically assign the IPs.
- Go to **Tools** right top corner and choose 'DHCP' from list.
  
![Standard)](images/lab-setup/40-dhcp.png)

- Right click 'IPv4' and
  
![Standard)](images/lab-setup/41-dhcp.png)

- Give name to scope
  
![Standard)](images/lab-setup/42-dhcp.png)

- Add IP address ranges
  
![Standard)](images/lab-setup/43-dhcp.png)

- Add 'Exclusions and Delay'
  The address that we don't want to give out

![Standard)](images/lab-setup/44-dhcp.png)

- 'Lease Duration'
  The time till a machine will hold the assigned IP address
  
![Standard)](images/lab-setup/45-dhcp.png)

- 'Configure DHCP Option'
  
![Standard)](images/lab-setup/47-dhcp.png)

- 'Router (Default Gateway)'
  Add IP address and click Add and then Next
  
![Standard)](images/lab-setup/48-dhcp.png)

- 'Domain Name and DNS Servers'
  
![Standard)](images/lab-setup/49-dhcp.png)

  Keep choosing default until Finsih

- Do right click the domain name and choose 'Authorize' and then refresh it.
- 
 ![Standard)](images/lab-setup/46-dhcp.png)


