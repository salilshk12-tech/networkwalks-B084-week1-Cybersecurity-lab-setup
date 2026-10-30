<div align="center">

# 🛡️ Cybersecurity Home Lab: VirtualBox + Kali Linux

**A private, isolated NAT Network lab for ethical hacking and penetration testing practice**

![VirtualBox](https://img.shields.io/badge/VirtualBox-7.x-183A61?style=for-the-badge&logo=virtualbox&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-2026.3-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=for-the-badge)
![Batch](https://img.shields.io/badge/Networkwalks-B084-C00000?style=for-the-badge)
![Status](https://img.shields.io/badge/Phase%201-Complete-brightgreen?style=for-the-badge)

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Project Requirements](#-project-requirements)
- [Lab Specifications](#-lab-specifications)
- [Network Architecture](#-network-architecture)
- [Setup Walkthrough](#-setup-walkthrough)
- [Screenshots](#-screenshots)
- [Verification](#-verification)
- [Troubleshooting](#-troubleshooting)
- [Key Takeaways](#-key-takeaways)
- [Phase 2 Roadmap](#-phase-2-roadmap)
- [Ethical Use](#-ethical-use-disclaimer)
- [Resources](#-resources)
- [Author](#-author)

---

## 📌 Overview

This repository documents **Week 1, Project Module 1 (WK1-PM1)** of my cybersecurity training with **Networkwalks (Batch B084)**: building a private virtual lab for ethical hacking practice.

**Kali Linux** acts as the attacker machine inside **VirtualBox**, connected to a custom **NAT Network (`10.0.0.0/24`)**. Kali uses a manually assigned static IP and has full internet access. The network is built to host additional target machines in later phases.

I'm a second-year B.Sc. Cybersecurity student, and I'm keeping this record of my setup, the problems I hit, and what I learned.

---

## 🎯 Project Requirements

- [x] VirtualBox used as the base hypervisor
- [x] Kali Linux set up as the attacking machine
- [x] Custom NAT Network created on `10.0.0.0/24`
- [x] Clipboard sharing and drag & drop enabled
- [x] Host `Downloads` folder shared with the Kali VM
- [x] Kali assigned the static IP `10.0.0.2/24`
- [x] Full internet access confirmed from Kali
- [x] Clean VM snapshot created

---

## 🧰 Lab Specifications

| Component | Details |
|---|---|
| Host OS | Windows 10 / 11 *(edit)* |
| Host Hardware | *(e.g. 8 GB RAM, Core i5, 256 GB SSD)* |
| Hypervisor | VirtualBox *(version)* |
| Guest OS | Kali Linux 2026.3 |
| Kali VM RAM | *(e.g. 2048 MB)* |
| Network Type | NAT Network (custom) |
| Network Name | `NatNetwork` |
| Subnet | `10.0.0.0/24` |
| Kali IP | `10.0.0.2/24` (static) |
| Gateway | `10.0.0.1` |
| DNS | `10.0.0.1` |
| Reserved Lab Range | `10.0.0.2 – 10.0.0.99` |

---

## 🗺️ Network Architecture

```text
 ┌───────────────────────────────────────────────────────┐
 │  Host Machine (Windows 10/11)                         │
 │                                                       │
 │   ┌───────────────────────────────────────────────┐   │
 │   │ VirtualBox: NatNetwork (10.0.0.0/24)          │   │
 │   │ Gateway: 10.0.0.1                             │   │
 │   │                                               │   │
 │   │   ┌──────────────────┐                        │   │
 │   │   │   Kali Linux     │  ← Attacker machine    │   │
 │   │   │   10.0.0.2/24    │                        │   │
 │   │   └──────────────────┘                        │   │
 │   │                                               │   │
 │   │   Future target VMs: 10.0.0.3 – 10.0.0.99     │   │
 │   └───────────────────────────────────────────────┘   │
 │                          │                            │
 └──────────────────────────┼────────────────────────────┘
                            ▼
                        Internet
```

---

## 🪜 Setup Walkthrough

### Step 1: Install 7-Zip
Kali's pre-built VirtualBox image ships as a compressed archive, so I installed 7-Zip to extract it.

### Step 2: Install VirtualBox
Downloaded from the official website and installed on the host.

### Step 3: Create the NAT Network
**File → Tools → Network → NAT Networks**

```text
Name        : NatNetwork
IPv4 Prefix : 10.0.0.0/24
DHCP        : Enabled
IPv6        : Disabled
```

> A NAT Network lets all attached VMs talk to each other and still reach the internet, which suits an attacker/target lab.

### Step 4: Import Kali Linux
Downloaded the official Kali 2026.3 VirtualBox image, extracted it with 7-Zip, and imported it.

```text
Network Adapter 1 : Attached to NAT Network
Network Name      : NatNetwork
Adapter Type      : Intel PRO/1000 MT Desktop
Promiscuous Mode  : Allow All
Shared Clipboard  : Bidirectional
Drag and Drop     : Bidirectional
Shared Folder     : Host "Downloads" (Auto-mount, Full access)
```

### Step 5: Configure the Static IP in Kali
Opened **Edit Connections → Wired connection 1 → IPv4 Settings**, set the method to **Manual**:

```text
Address : 10.0.0.2
Netmask : 24
Gateway : 10.0.0.1
DNS     : 10.0.0.1
```

### Step 6: Fix the connection delay (DAD timeout)
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

### Step 7: Take a Snapshot
After confirming everything worked, I saved a snapshot:

```text
Clean Kali - Network Configured
```

This gives me a safe baseline to restore if I break something later.

---

## 📸 Screenshots

### 1. NAT Network settings
<img src="VirtualBox_kali-linux-2026.3-virtualbox-amd64_REPLACE_1.png" alt="NAT Network settings" width="800">

### 2. Kali VM settings
<img src="VirtualBox_kali-linux-2026.3-virtualbox-amd64_REPLACE_2.png" alt="Kali VM settings" width="800">

### 3. Kali IP configuration and ping test
<img src="VirtualBox_kali-linux-2026.3-virtualbox-amd64_REPLACE_3.png" alt="Kali IP configuration and ping test" width="800">

### 4. Static IPv4 configuration in Kali
<img src="IMG-20261030-WA0076.jpg" alt="Static IPv4 settings in Kali" width="800">

### 5. Applying the DAD timeout fix
<img src="IMG-20261030-WA0075.jpg" alt="nmcli DAD timeout fix in terminal" width="800">

---

## ✅ Verification

| Test | Command | Expected Result |
|---|---|---|
| Check IP | `ip a` | Shows `10.0.0.2/24` |
| Ping gateway | `ping -c 4 10.0.0.1` | Replies received |
| Ping internet | `ping -c 4 8.8.8.8` | Replies received |
| DNS lookup | `nslookup google.com` | Domain resolves |
| Tool check | `nmap --version` | Version displayed |
| Shared folder | `ls /media/sf_Downloads` | Host files visible |

---

## 🐞 Troubleshooting

### Problem: No internet after setting the static IP
**Cause:** A known issue with VirtualBox 7 and newer Kali releases, where NetworkManager's duplicate address detection (DAD) delays the connection.

**Fix:**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

Then restart Kali and test again.

**If it still fails:**
- Confirm the NAT Network exists and is attached to the VM
- Make sure no other VM uses `10.0.0.2`
- Try `8.8.8.8` as the DNS server

### Problem: *(add your own, or delete this section)*
- **What happened:** …
- **How I fixed it:** …

---

## 📚 Key Takeaways

- **NAT vs NAT Network:** plain NAT isolates each VM; a NAT Network lets VMs talk to each other and still reach the internet.
- **Static addressing:** how IP, netmask, gateway, and DNS work together.
- **Systematic troubleshooting:** test IP → gateway → internet → DNS to find where connectivity breaks.
- **Snapshots:** a clean baseline makes experimenting safe.
- **Documentation:** recording every step is part of doing security work properly.

---

## 🔭 Phase 2 Roadmap

| Machine | Planned IP | Status |
|---|---|---|
| Kali Linux (attacker) | 10.0.0.2 | ✅ Done |
| Windows 10 VM | 10.0.0.10 | ⬜ Planned |
| Windows 11 VM | 10.0.0.11 | ⬜ Planned |
| Windows 7 VM | 10.0.0.7 | ⬜ Planned |
| Android VM | 10.0.0.9 | ⬜ Planned |
| Windows Server 2016 | 10.0.0.16 | ⬜ Planned |

**Next goals:** ping tests between all machines, snapshots of each, and Nmap scanning practice.

---

## ⚠️ Ethical Use Disclaimer

This lab is for **education and legal practice only**. I only test systems that I own or have explicit permission to test. Using these tools against anyone else's systems is illegal and unethical.

---

## 🔗 Resources

- [7-Zip](https://7-zip.org/download.html)
- [VirtualBox Downloads](https://virtualbox.org/wiki/Downloads)
- [Kali Linux Downloads](https://kali.org/get-kali)

---

## 👤 Author

**Your Name**
B.Sc. Cybersecurity Student (Year 2) | Networkwalks Batch B084

[LinkedIn](https://linkedin.com/in/your-profile) • [GitHub](https://github.com/salilshk12-tech)

---

<div align="center">

*Part of my cybersecurity learning journey. Updated as the lab grows.*

</div>
