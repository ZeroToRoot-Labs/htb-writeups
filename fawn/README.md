# Fawn – Hack The Box Starting Point

## Overview

**Difficulty:** Very Easy  
**OS:** Linux  
**Category:** Starting Point  
**Focus:** FTP, anonymous login, basic enumeration
**YouTube Video:** Coming soon

Fawn introduces the FTP service and shows how misconfigured anonymous access can expose sensitive files.

---

## 1. Environment setup

- Connected to HTB via OpenVPN:

```bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn

Verified VPN interface:

bash
ip a   # checked for tun0
Target IP (from HTB panel):
