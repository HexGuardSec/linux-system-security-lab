# Scenario 08 – Unauthorized Privilege Modification Attempt

## 🧩 Context

This scenario simulates a real-world security incident where a regular user attempts to access or manipulate privileged system files or binaries.

We will analyze unauthorized attempts on sensitive files (`/etc/shadow`, `/etc/sudoers`) and inspect SUID/SGID binaries that could be abused for privilege escalation.

---

## 🧪 Step-by-Step Reproduction

### 1. Create a regular user

```bash
sudo adduser paul
````

---

### 2. Attempt privilege escalation as `paul`

From the new user account, simulate these actions:

```bash
cat /etc/shadow
cat /etc/sudoers
sudo ls /root
```

Expected results: `Permission denied`

> ✅ Screenshot: **05-shadow-access-denied.png**
> ✅ Screenshot: **07-sudoers-permissions-denied.png**

---

### 3. Analyze log files for denied actions

```bash
sudo journalctl -xe | grep paul
sudo grep 'denied' /var/log/auth.log
```

Identify failed access attempts or authentication issues.

> 📝 *Include screenshots in future if useful — optional here.*

---

### 4. Review file permissions of sensitive files

```bash
ls -l /etc/passwd /etc/shadow /etc/sudoers
```

> ✅ Screenshot: **04-passwd-shadow-permissions.png**
> ✅ Screenshot: **06-critical-file-permissions.png**

---

### 5. Audit all SUID and SGID binaries

List all SUID binaries:

```bash
sudo find /bin /usr/bin -perm -4000 -exec ls -l {} \;
```

List all SGID binaries:

```bash
sudo find /bin /usr/bin -perm -2000 -exec ls -l {} \;
```

> ✅ Screenshot: **01-list-suid.png**
> ✅ Screenshot: **02-list-sgid.png**
> ✅ Screenshot: **08-suid-quick-audit.png**

---

### 6. Create and test a fake SUID shell

```bash
sudo mkdir -p /opt/test-suid
sudo cp /bin/bash /opt/test-suid/rootshell
sudo chmod u+s /opt/test-suid/rootshell
```

Try running:

```bash
./rootshell
whoami
```

> Expected result: On modern systems (Bash ≥ 4.2), effective UID is not changed.
> ✅ Screenshot: **03-fake-suid-shell.png**

---

## 📌 System Environment

* OS: Ubuntu Server 24.04 LTS
* User: `paul`
* Kernel: `uname -r`

---

## 🧠 Lessons Learned

* SUID/SGID binaries are powerful but dangerous.
* Regular users should never access `/etc/shadow` or `/etc/sudoers`.
* Linux logs (`auth.log`, `journalctl`) help trace unauthorized activity.
* Fake shells can be created but are limited on secure systems.

---

## ✅ Fixes

* Audit SUID/SGID: `find / -perm -4000`
* Harden sudoers: `chmod 440 /etc/sudoers`
* Monitor with Fail2ban, auditd, or manual log review

---

## 📸 Screenshots Summary

```
01-list-suid.png  
02-list-sgid.png  
03-fake-suid-shell.png  
04-passwd-shadow-permissions.png  
05-shadow-access-denied.png  
06-critical-file-permissions.png  
07-sudoers-permissions-denied.png  
08-suid-quick-audit.png
```