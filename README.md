<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>🧰 Environments & Technologies Used</h2>

- **Microsoft Azure (Virtual Machines)**
- **Remote Desktop (RDP)**
- **Wireshark (Protocol Analyzer)**
- **Command-Line Tools (PowerShell, SSH, nslookup, etc.)**
- **Network Protocols:** ICMP, SSH, DHCP, DNS, RDP

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>🔧 Three High-Level Configuration & Observation Steps</h2>

1. ☁️ Deploy Azure Virtual Machines
2. 📡 Capture and Observe ICMP Traffic with Wireshark
3. 🔒 Configure Network Security Groups (NSGs) and Observe Effects

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

### 1. ☁️ Deploy Azure Virtual Machines

- Created a new **Resource Group** in the Azure Portal.
- Deployed a **Windows 10 VM**, allowing Azure to auto-create:
  - New **Virtual Network (VNet)**
  - New **Subnet**
- Deployed a **Linux (Ubuntu Server) VM** into the **same VNet/Subnet**.
- Verified both VMs were connected to the same network and ready for communication testing.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

### 2. 📡 Capture and Observe ICMP Traffic with Wireshark

- Installed **Wireshark** on the Windows 10 VM via RDP.
- Started a live capture with filter: `icmp`
- Used `ping` from Windows VM to:
  - Ubuntu VM's **private IP** (to observe internal ICMP).
  - `www.google.com` (to observe external ICMP).
- Verified ICMP echo requests and replies within Wireshark's interface.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

### 3. 🔒 Configure Network Security Groups (NSGs) and Observe Effects

- Initiated continuous ping (`ping -t`) from Windows VM to Ubuntu VM.
- Modified the **NSG for the Ubuntu VM**:
  - **Disabled inbound ICMP** → Verified pings started failing.
  - **Re-enabled inbound ICMP** → Verified pings resumed.
- Observed traffic behavior changes live in Wireshark.

- **Observed Protocols in Action:**
  - **SSH Traffic:**
    - Ran: `ssh labuser@<ubuntu-vm-private-ip>`
    - Interacted with Ubuntu via SSH and filtered with `ssh` in Wireshark.
  - **DHCP Traffic:**
    - Filtered with `bootp` (Wireshark alias for DHCP).
    - Ran: `ipconfig /renew` in PowerShell to request a new IP.
  - **DNS Traffic:**
    - Filtered with `dns`
    - Used `nslookup google.com` and `nslookup disney.com`
  - **RDP Traffic:**
    - Filtered with `tcp.port == 3389`
    - Observed constant stream of data due to the nature of the RDP session.
<br />
## 💼 Skills Demonstrated

- Azure Virtual Machine deployment and virtual networking
- Configuration and testing of **Network Security Groups (NSGs)**
- Use of **Wireshark** for packet inspection
- Hands-on experience with core **network protocols**:
  - ICMP, SSH, DHCP, DNS, RDP
- Remote administration via **RDP** and **SSH**
- Real-time protocol analysis for troubleshooting and validation
