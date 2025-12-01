# 02 – SSH Hardening and Access Control

## 🎯 Objective
This module focuses on securing SSH access and analyzing SSH authentication behavior.  
It includes configuration, hardening, log analysis, and troubleshooting real SSH connection scenarios.

---

## 📌 Topics Covered

### ✔️ SSH Key Authentication
- Generating SSH keys
- Deploying public keys (`ssh-copy-id`)
- Testing passwordless authentication

### ✔️ Hardening Strategies
- Changing default SSH port
- Disabling password authentication
- Disabling keyboard-interactive login
- Understanding `sshd_config.d` precedence

### ✔️ Troubleshooting Scenarios
- Wrong shell (`/bin/false`)
- Missing home directory
- Invalid authorized_keys permissions
- Expired or missing keys

### ✔️ Log Analysis
- `/var/log/auth.log`
- `journalctl -u ssh`
- `sshd -T` (active configuration)

---

## 📂 Files
- `configs/` — sshd_config before/after hardening  
- `documentations/` — detailed explanations (password security, SSH hardening)  
- `screenshots/` — all steps executed  

---

## 🧠 Skills Demonstrated
- SSH security  
- Access troubleshooting  
- Linux authentication mechanism  
- System logging and debugging  