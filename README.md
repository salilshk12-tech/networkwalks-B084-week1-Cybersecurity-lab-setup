# networkwalks-B084-week1-Cybersecurity-lab-setup
🛡️ Cybersecurity Lab Setup: VirtualBox + Kali Linux

An isolated virtual lab for ethical hacking and penetration testing practice.

"VirtualBox" (https://img.shields.io/badge/VirtualBox-7.x-183A61?style=flat-square&logo=virtualbox&logoColor=white)
"Kali Linux" (https://img.shields.io/badge/Kali%20Linux-2026.3-557C94?style=flat-square&logo=kalilinux&logoColor=white)
"Network" (https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square)
"Batch" (https://img.shields.io/badge/Networkwalks-B084-C00000?style=flat-square)
"Status" (https://img.shields.io/badge/Status-Phase%201%20Complete-brightgreen?style=flat-square)

---

📌 Overview

This repository documents Week 1, Project 1 of my cybersecurity training with Networkwalks (Batch B084).

The objective was to build a virtual cybersecurity lab using Oracle VirtualBox and Kali Linux.

I configured Kali Linux as my attacker machine using a custom NAT Network with the subnet "10.0.0.0/24".

The lab uses a static IP address, allowing additional virtual machines to be connected in future phases for penetration testing and network security practice.

As a second-year B.Sc. Cybersecurity student, I'm documenting my practical learning experience, configurations, troubleshooting steps and technical knowledge.

---

🎯 Project Requirements

- [x] Install Oracle VirtualBox.
- [x] Import Kali Linux 2026.3.
- [x] Create a custom NAT Network.
- [x] Configure the network subnet "10.0.0.0/24".
- [x] Configure Kali Linux with a static IP address.
- [x] Configure gateway and DNS.
- [x] Enable clipboard sharing and drag & drop.
- [x] Configure a shared folder.
- [x] Create a clean virtual machine snapshot.
- [x] Configure NetworkManager to resolve the connectivity issue.

---

🧰 Lab Specifications

Component| Configuration
Host OS| Windows
Hypervisor| Oracle VirtualBox
Guest OS| Kali Linux 2026.3
Network Type| NAT Network
Network Name| NatNetwork
Subnet| 10.0.0.0/24
Kali IP Address| 10.0.0.2
Subnet Mask| 255.255.255.0 (/24)
Default Gateway| 10.0.0.1
DNS Server| 10.0.0.1
DHCP| Enabled at NAT Network level
VM Name| fresh kali linux

---

🗺️ Network Architecture

          HOST MACHINE (WINDOWS)
                    |
                    |
              VIRTUALBOX
                    |
                    |
          NAT NETWORK (NatNetwork)
               10.0.0.0/24
                    |
              Gateway
               10.0.0.1
                    |
          ---------------------
          |                   |
      KALI LINUX          FUTURE VMs
       ATTACKER             TARGETS
      10.0.0.2          10.0.0.3-99
          |
          |
       INTERNET

---

🪜 Setup Walkthrough

Step 1: Install 7-Zip

Installed 7-Zip to extract the downloaded Kali Linux VirtualBox archive.

Step 2: Install Oracle VirtualBox

Downloaded and installed Oracle VirtualBox to create and manage virtual machines.

Step 3: Create NAT Network

Navigated to:

"VirtualBox → File → Tools → Network → NAT Networks"

Created a custom NAT Network with the following configuration:

Network Name : NatNetwork
IPv4 Prefix  : 10.0.0.0/24
DHCP         : Enabled
IPv6         : Disabled

A NAT Network allows connected virtual machines to communicate with each other while accessing the internet through NAT.

Step 4: Import Kali Linux

Downloaded the official Kali Linux 2026.3 VirtualBox image, extracted the archive and imported the virtual machine.

Configured the following settings:

Network Adapter : NAT Network
Network Name    : NatNetwork
Shared Clipboard: Bidirectional
Drag and Drop   : Bidirectional
Shared Folder   : Downloads

Step 5: Configure Static IP Address

Opened Network Manager in Kali Linux and selected:

"Wired Connection 1 → IPv4 Settings → Manual"

Configured the following:

Address : 10.0.0.2
Netmask : 24
Gateway : 10.0.0.1
DNS     : 10.0.0.1

This assigns a static IP address to the Kali Linux machine.

Step 6: Resolve Network Connectivity Issue

While configuring the network, I encountered a connectivity issue.

I used the following command to modify the NetworkManager connection:

sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

This changes the IPv4 Duplicate Address Detection timeout.

Step 7: Create Virtual Machine Snapshot

Created a snapshot of the Kali Linux virtual machine to preserve the configured environment and provide a recovery point for future experiments.

---

📸 Project Screenshots

1. VirtualBox Manager

Virtual machine management and snapshot configuration.

"VirtualBox Manager" (screenshots/1000267552.jpg)

2. Kali Linux Desktop

Successfully booted Kali Linux virtual machine.

"Kali Linux Desktop" (screenshots/1000267553.jpg)

3. Static IP Configuration

Manual IPv4 configuration with static IP, subnet mask and gateway.

"IPv4 Configuration" (screenshots/1000267554.jpg)

4. NetworkManager Configuration

Executing the NetworkManager command to modify the IPv4 DAD timeout.

"Terminal Configuration" (screenshots/1000267555.jpg)

5. GitHub Repository

Project documentation and repository structure.

"GitHub Repository" (screenshots/1000267556.jpg)

---

🔍 Network Verification Commands

The following commands can be used to verify the network configuration:

Purpose| Command
Check IP address| "ip a"
Check routing table| "ip route"
Ping gateway| "ping -c 4 10.0.0.1"
Test internet connectivity| "ping -c 4 8.8.8.8"
Test DNS resolution| "nslookup google.com"
Check Nmap version| "nmap --version"

---

🐞 Problems Faced & Troubleshooting

Problem 1: Network Connectivity Issue

Issue: Encountered a connectivity issue after configuring the static IPv4 address.

Solution: Modified the IPv4 DAD timeout using NetworkManager.

sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

Problem 2: Static IP Configuration

Issue: Needed a fixed IP address for the attacker machine.

Solution: Configured IPv4 manually through Network Manager.

IP Address : 10.0.0.2
Gateway    : 10.0.0.1
Netmask    : 255.255.255.0

---

📚 Key Learnings

Through this project, I learned:

1. How to install and configure Oracle VirtualBox.
2. How to import and manage Kali Linux virtual machines.
3. Difference between NAT and NAT Network.
4. Understanding IPv4 addressing and subnet masks.
5. Configuring static IP addresses.
6. Understanding gateways and DNS servers.
7. Basic Linux networking commands.
8. Troubleshooting network connectivity using NetworkManager.
9. Importance of virtual machine snapshots.
10. Building an isolated environment for ethical hacking practice.

---

🔭 Phase 2: Future Plans

The next phase involves adding multiple target machines to the same virtual network.

Machine| Planned IP| Status
Kali Linux (Attacker)| 10.0.0.2| ✅ Completed
Windows 10| 10.0.0.10| ⬜ Planned
Windows 11| 10.0.0.11| ⬜ Planned
Windows 7| 10.0.0.7| ⬜ Planned
Android VM| 10.0.0.9| ⬜ Planned
Windows Server 2016| 10.0.0.16| ⬜ Planned

Upcoming Activities

- Configure target virtual machines.
- Establish communication between virtual machines.
- Perform network discovery using Nmap.
- Practice port scanning.
- Understand open ports and running services.
- Perform vulnerability assessment in the isolated lab.

---

⚠️ Ethical Use Disclaimer

This project is strictly for educational purposes and authorized cybersecurity testing.

All penetration testing and security experiments will be performed only on systems that I own or have explicit permission to test.

---

🔗 Resources

- "Kali Linux Official Website" (https://www.kali.org/)
- "Oracle VirtualBox" (https://www.virtualbox.org/wiki/Downloads)
- "7-Zip" (https://www.7-zip.org/)
- "NetworkManager Documentation" (https://networkmanager.dev/docs/)

---

👨‍💻 Author

Salil Zameer Shaikh

B.Sc. Cybersecurity Student | Second Year
Networkwalks – Batch B084

- GitHub: "salilshk12-tech" (https://github.com/salilshk12-tech)
- LinkedIn: Add your LinkedIn profile URL here.

---

<div align="center">Learning. Practicing. Securing.

Documenting my journey into Cybersecurity and Ethical Hacking.

</div>
