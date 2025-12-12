Home-Network-Security-Assessment

## Description
This project documents a basic security assessment of my home network.
The goal was to identify active devices, analyse exposed services and
apply simple security hardening to reduce the local attack surface.

This assessment was conducted from a defensive (blue team) perspective
and focused on understanding normal network behaviour before applying
mitigations.

---

## Network Environment
- Operating System: Windows 11
- Network Type: Home Wi-Fi (Private Network)
- Router / Default Gateway: 192.168.1.1
- Local Subnet: 192.168.1.0/24
- Tools Used: ipconfig, nmap

---

## Methodology
The assessment was done in the following steps:

1. Identified local network configuration using `ipconfig`
2. Determined the active subnet and default gateway
3. Performed host discovery to identify active devices using `nmap`
4. Conducted a limited TCP SYN port scan on my own device
5. Analysed exposed services and assessed the potential risk
6. Applied security mitigations to reduce exposure
7. Re-scanned to verify the effectiveness of mitigations

---

## Findings

### Device Discovery
Three devices were identified on this network:
- Router (192.168.1.1)
- Personal Computer (192.168.1.2)
- Secondary device (192.168.1.4)

No unexpected or unknown devices were observed during the scan.

---

### Port Scan Results (Before Mitigation)
A TCP SYN scan of ports 1–1000 on my PC identified the following open services:

- 135/tcp – Microsoft RPC
- 139/tcp – NetBIOS Session Service
- 445/tcp – SMB (Microsoft-DS)

The majority of scanned ports were closed or filtered, indicating a
limited initial attack surface.

---

## Risk Analysis
NetBIOS and SMB services are commonly targeted if exposed to untrusted
networks. While these services were only accessible on the local network,
they were not required for my use case and increased the potential
attack surface of the system.

If misconfigured or exposed to public networks, these services could
lead to unauthorised access or movement.

---

## Mitigations Applied
The following mitigations were implemented to reduce risk:

- Disabled Windows file and printer sharing
- Disabled legacy SMBv1 support
- Confirmed Windows Firewall was enabled for both private and public profiles
- Ensured file sharing related firewall rules were restricted to private networks only

---

## What I Learned
This project helped me better understand how devices communicate on a
local network, how exposed services increase security risk and how
simple configuration changes can significantly improve host security.

