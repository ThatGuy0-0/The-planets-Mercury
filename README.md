# 🛰️ The Planets: Mercury – VulnHub Walkthrough

**Difficulty:** Easy  
**Author:** SirFlash  
**Platform:** VulnHub  
**Objective:** Gain root access and retrieve both user and root flags.

---

## 🚀 Overview

Mercury is a beginner-friendly boot2root virtual machine hosted on VulnHub. The goal is to leverage enumeration, SQL injection, SSH login, and privilege escalation techniques to retrieve two flags.

---

## 🧰 Tools Used

- Kali Linux  
- netdiscover  
- nmap  
- sqlmap  
- wfuzz  
- SSH client  
- Text editors (nano, vim)  
- `sudo --preserve-env`

---

## 🧭 Steps to Exploit

### 1. 🔍 Network Discovery

Use `netdiscover` to find the target's IP address:

```bash
netdiscover -r 192.168.56.0/24
