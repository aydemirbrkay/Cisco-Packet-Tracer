<div align="center">

# 🏛️ University Campus Network Design

### Üniversite Kampüs Ağı Tasarımı Projesi

[![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-0076CE?style=for-the-badge&logo=cisco&logoColor=white)](https://www.netacad.com/courses/packet-tracer)
[![LaTeX](https://img.shields.io/badge/LaTeX-Documentation-008080?style=for-the-badge&logo=latex&logoColor=white)](docs/main.tex)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

*An end-to-end enterprise campus network infrastructure designed and simulated in Cisco Packet Tracer*

**Erciyes Üniversitesi • Bilgisayar Mühendisliği • Design Project • 2025-2026**

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Network Architecture](#-network-architecture)
- [Features](#-features)
- [IP Addressing Scheme](#-ip-addressing-scheme)
- [Project Structure](#-project-structure)
- [Configurations](#%EF%B8%8F-configurations)
- [Testing & Validation](#-testing--validation)
- [Documentation](#-documentation)
- [Author](#-author)

---

## 🔍 Overview

This project encompasses the complete design and simulation of a **university campus network** for Erciyes University. The network architecture provides reliable, modular, scalable, and highly available enterprise network infrastructure serving multiple faculties, administrative departments, and server rooms.

The campus network is designed with industry-standard **three-tier hierarchical model** (Core, Distribution, Access) and implements modern networking technologies including VLAN segmentation, OSPF dynamic routing, HSRP redundancy, VoIP integration, Site-to-Site VPN, and comprehensive security measures.

---

## 🏗️ Network Architecture

```
                          ┌─────────────┐
                          │  Internet    │
                          │  (ISP Cloud) │
                          └──────┬───────┘
                                 │
                    ╔════════════╧════════════╗
                    ║      CORE LAYER         ║
                    ║  XYZ-ENG-R  XYZ-SRV-R   ║
                    ║  XYZ-TIP-R  XYZ-EDB-R   ║
                    ╚════════════╤════════════╝
                                 │
                    ╔════════════╧════════════╗
                    ║   DISTRIBUTION LAYER    ║
                    ║  ENG-MLS1/2  SRV-MLS1/2 ║
                    ║  TIP-MLS1/2  EDB-MLS1/2 ║
                    ╚════════════╤════════════╝
                                 │
                    ╔════════════╧════════════╗
                    ║     ACCESS LAYER        ║
                    ║  Faculty Switches (24p)  ║
                    ║  APs, Phones, Printers   ║
                    ╚═════════════════════════╝
```

### Faculties & Departments

| Faculty | Departments | Users |
|---------|------------|-------|
| 🏗️ **Engineering** | 13 departments (Civil, Mechanical, EE, CS, Software, Industrial, Environmental, Mechatronics, Geomatics, Biomedical, Food, Textile, Energy) | 30–252 per dept |
| 🏥 **Medicine** | Lab, Radiology, Anatomy, Pharmacology | 62 per dept |
| 📚 **Literature** | TDE, RDE | 62 per dept |
| 🖥️ **Server Room** | Web, Email, DNS, 2×DHCP Servers | — |
| 🏢 **Admin** | IT Department, Finance | 252 per dept |

---

## ✨ Features

| Feature | Technology | Description |
|---------|-----------|-------------|
| 🔀 **VLAN Segmentation** | IEEE 802.1Q | Logical isolation for each department |
| 🌐 **Dynamic Routing** | OSPF | Optimal path selection using Dijkstra algorithm |
| 🔄 **High Availability** | HSRP | Redundant gateway with automatic failover |
| 📞 **VoIP Integration** | CME / SCCP | IP telephony with auto-registration |
| 🔒 **VPN** | IPsec Site-to-Site | Encrypted tunnel between campus and server farm |
| 🛡️ **Security** | ACL, Port Security, SSH | Multi-layer access control |
| 📡 **Wireless** | WLC + LAP | Centralized wireless management |
| ⚡ **Link Aggregation** | LACP | EtherChannel for increased bandwidth |
| 🌍 **NAT/PAT** | Overload NAT | Multiple users sharing single public IP |
| 📋 **IP Management** | DHCP + DNS | Centralized IP and name resolution |

---

## 📊 IP Addressing Scheme

### Engineering Faculty (192.168.10.0 – 192.168.15.x)

| Department | Network | Subnet Mask | Max Hosts |
|-----------|---------|-------------|-----------|
| Civil Eng. | 192.168.10.0/24 | 255.255.255.0 | 254 |
| Mechanical Eng. | 192.168.11.0/24 | 255.255.255.0 | 254 |
| Electrical-Electronics | 192.168.12.0/24 | 255.255.255.0 | 254 |
| Computer Eng. | 192.168.13.0/24 | 255.255.255.0 | 254 |
| Software Eng. | 192.168.14.0/26 | 255.255.255.192 | 62 |
| Industrial Eng. | 192.168.14.64/26 | 255.255.255.192 | 62 |
| Environmental Eng. | 192.168.14.128/26 | 255.255.255.192 | 62 |
| Mechatronics Eng. | 192.168.14.192/26 | 255.255.255.192 | 62 |
| Geomatics Eng. | 192.168.15.0/27 | 255.255.255.224 | 30 |
| Biomedical Eng. | 192.168.15.32/27 | 255.255.255.224 | 30 |
| Food Eng. | 192.168.15.64/27 | 255.255.255.224 | 30 |
| Textile Eng. | 192.168.15.96/27 | 255.255.255.224 | 30 |
| Energy Eng. | 192.168.15.128/27 | 255.255.255.224 | 30 |

### Server & Admin (192.168.16.0 – 192.168.18.x)

| Department | Network | Max Hosts |
|-----------|---------|-----------|
| IT Department | 192.168.16.0/24 | 254 |
| Finance | 192.168.17.0/24 | 254 |
| Server Room | 192.168.18.0/28 | 14 |

### Medicine (192.168.20.x) & Literature (192.168.21.x)

| Department | Network | Max Hosts |
|-----------|---------|-----------|
| Med-Lab | 192.168.20.0/26 | 62 |
| Med-Radiology | 192.168.20.64/26 | 62 |
| Med-Anatomy | 192.168.20.128/26 | 62 |
| Med-Pharmacology | 192.168.20.192/26 | 62 |
| Lit-TDE | 192.168.21.0/26 | 62 |
| Lit-RDE | 192.168.21.64/26 | 62 |

---

## 📁 Project Structure

```
📦 University-Campus-Network-Design/
├── 📄 README.md                          # This file
├── 📄 .gitignore                         # Git ignore rules
├── 📄 Design Project Report.pdf          # Original project report
│
├── 📂 configs/                           # Cisco IOS Configuration Files
│   ├── 01-basic-device.ios               # Hostname, SSH, ACL, password
│   ├── 02-stp-bpduguard.ios              # STP PortFast + BPDU Guard
│   ├── 03-vlan-trunk-access.ios          # VLAN, Trunk, Access ports
│   ├── 04-distribution-layer.ios         # MLS VLAN definitions
│   ├── 05-lacp-etherchannel.ios          # LACP EtherChannel
│   ├── 06-port-security.ios              # MAC-based port security
│   ├── 07-voip-subinterface.ios          # VoIP sub-interface
│   ├── 08-hsrp.ios                       # HSRP redundancy
│   ├── 09-dhcp-helper.ios                # DHCP relay (ip helper)
│   ├── 10-ospf.ios                       # OSPF routing
│   ├── 11-voip-telephony.ios             # CME / VoIP service
│   ├── 12-nat-pat.ios                    # NAT/PAT overload
│   └── 13-vpn-ipsec.ios                  # Site-to-Site IPsec VPN
│
└── 📂 docs/                              # LaTeX Documentation
    ├── main.tex                          # Main LaTeX source (TikZ diagrams)
    └── 📂 figures/                       # Topology & test screenshots
        ├── topology-overview-1.png
        ├── topology-overview-2.png
        ├── test-dhcp-dns.png
        ├── test-pat-vpn.png
        ├── test-hsrp-voip.png
        ├── test-voip-icmp.png
        ├── test-icmp-ssh.png
        └── test-ssh.png
```

---

## ⚙️ Configurations

All Cisco IOS configurations are organized in the `configs/` directory with numbered prefixes for logical ordering:

| # | File | Description |
|---|------|-------------|
| 01 | `basic-device.ios` | Base security: hostname, passwords, SSH, ACL |
| 02 | `stp-bpduguard.ios` | STP PortFast + BPDU Guard for edge ports |
| 03 | `vlan-trunk-access.ios` | VLAN creation, trunk/access port assignments |
| 04 | `distribution-layer.ios` | MLS VLAN definitions (13 engineering depts) |
| 05 | `lacp-etherchannel.ios` | LACP link aggregation (3×1Gbps) |
| 06 | `port-security.ios` | Sticky MAC, max 2 devices, violation shutdown |
| 07 | `voip-subinterface.ios` | Router sub-interface for Voice VLAN 200 |
| 08 | `hsrp.ios` | Hot Standby Router Protocol (Active/Standby) |
| 09 | `dhcp-helper.ios` | IP helper-address for all VLANs |
| 10 | `ospf.ios` | OSPF Area 0 backbone routing |
| 11 | `voip-telephony.ios` | CME telephony service with auto-assign |
| 12 | `nat-pat.ios` | PAT overload for internet access |
| 13 | `vpn-ipsec.ios` | Site-to-Site IPsec VPN (AES-128, SHA) |

---

## 🧪 Testing & Validation

The following tests were performed to validate the network:

| Test | Status | Description |
|------|--------|-------------|
| ✅ DHCP | Passed | Dynamic IP assignment from central DHCP server |
| ✅ DNS | Passed | Domain name resolution (`erü.öbs`) |
| ✅ PAT/NAT | Passed | Internet access through PAT overload |
| ✅ VPN | Passed | Encrypted Site-to-Site tunnel verified via traceroute |
| ✅ HSRP | Passed | Active/Standby failover working correctly |
| ✅ VoIP | Passed | Auto phone registration and inter-faculty calls |
| ✅ ICMP | Passed | Cross-faculty ping connectivity |
| ✅ SSH | Passed | Remote secure access (IT dept only via ACL) |

---

## 📖 Documentation

The project includes comprehensive **LaTeX documentation** with:

- 📐 **TikZ network diagrams** (3-tier hierarchy, VLAN segmentation, HSRP, OSPF, VPN, EtherChannel, NAT/PAT)
- 📊 Complete **IP subnetting tables**
- 💻 All **Cisco IOS configurations** with syntax highlighting
- 📸 **Test screenshots** from Cisco Packet Tracer
- 🎨 Professional formatting with Erciyes University branding

### Building the LaTeX Document

```bash
cd docs/
pdflatex main.tex
pdflatex main.tex  # Run twice for TOC
```

---

## 👤 Author

**Berkay Aydemir**
- 📧 Student ID: 1030521387
- 🏫 Erciyes University — Computer Engineering
- 📚 Course: Design Project (2025–2026 Fall Semester)
- 👨‍🏫 Supervisor: Doç. Dr. Serkan ÖZTÜRK

---

<div align="center">

*Built with ❤️ using Cisco Packet Tracer and LaTeX*

</div>
