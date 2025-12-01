# 03 – System Enumeration & Security Audit

## 🎯 Objective
This module performs a complete enumeration of a Linux system, similar to what is done during security audits or troubleshooting.

This is essential knowledge for any SysAdmin or Internal IT Engineer.

---

## 📌 Topics Covered

### ✔️ System Information
- Kernel version
- OS release
- Hostname
- `uname -a`

### ✔️ User & Privilege Enumeration
- `id`, `groups`
- `/etc/passwd` and `/etc/shadow` permissions
- sudo rights (`sudo -l`)

### ✔️ Process Enumeration
- `ps aux`
- `ps -o pid,user,cmd,stat`

### ✔️ Service Enumeration
- `systemctl --type=service`
- Checking active/inactive services

### ✔️ Network Inspection
- `ip a`
- `ip route`
- `ss -tulnp`

### ✔️ SUID/SGID Binaries
- `find / -perm -4000 2>/dev/null`
- Understanding privilege escalation risks

---

## 📂 Files
- `screenshots/` — all enumerations captured  
- No configs for this module  

---

## 🧠 Skills Demonstrated
- Linux system audit  
- Security enumeration  
- Process & network inspection  
- Understanding privilege boundaries  