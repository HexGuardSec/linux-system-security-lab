# Scenario 01 – SSH Log Analysis

## 🎯 Objective

Analyze SSH activity and authentication attempts using Linux logs.  
This scenario simulates real-world access patterns (invalid user, failed login, successful access) and teaches how to audit SSH sessions using `/var/log/auth.log`, `journalctl`, and classic tools like `last`.

---

## 🧪 Test Cases & Log Extraction

### ✅ 1. Invalid User Attempt

- Simulated SSH attempt using a non-existent user `hackeruser`
- SSH output: `Permission denied`
- Command:
  ```bash
  sudo grep "Invalid user" /var/log/auth.log
````

* 📸 Screenshot: `01-illegal-user.png`

---

### ✅ 2. Failed Password (Wrong Credentials)

* SSH login with `staffuser`, but wrong password (2x)
* Command:

  ```bash
  sudo grep "Failed password" /var/log/auth.log
  ```
* 📸 Screenshot: `02-auth-failed.png`

---

### ✅ 3. Successful Login

* Valid credentials used for `staffuser`
* Command:

  ```bash
  sudo grep "Accepted password" /var/log/auth.log
  ```
* 📸 Screenshot: `03-auth-success.png`

---

### ✅ 4. Root Activity Detection

* Activity log when `itadmin` used `sudo`
* Command:

  ```bash
  sudo grep "session opened for user root by itadmin" /var/log/auth.log
  ```
* 📸 Screenshot: `04-root-activity.png`

---

### ✅ 5. Login and Reboot History

* Displays login attempts and system reboot events
* Commands:

  ```bash
  last -a
  last reboot
  ```
* 📸 Screenshot: `05-last-reboot.png`

---

### ✅ 6. SSH Logs via journalctl

* View systemd-level SSH logs (more detailed than auth.log)
* Command:

  ```bash
  sudo journalctl -u ssh
  ```
* 📸 Screenshot: `06-journalctl-ssh.png`

---

## 🧠 Key Learnings

* Understand Linux authentication flow
* Analyze login attempts using logs
* Monitor root activity and SSH behavior
* Master tools: `auth.log`, `journalctl`, `last`

---

## 📁 Files

* Screenshots: `/screenshots/01-log-analysis/`
* No code/script in this scenario

---

## 🔒 Notes

* `fail2ban` was **temporarily disabled** to allow brute-force simulation
* Password authentication was enabled in `sshd_config` for testing