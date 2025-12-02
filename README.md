# Linux System Security Lab

This project is a complete hands-on Linux system security and administration lab.  
It combines user management, SSH security, system enumeration, and service auditing into one structured learning environment.

It demonstrates practical skills required for:
- Junior SysAdmin roles
- Internal IT Engineer positions
- Linux support and security operations

This repo merges three previous labs into a single, enterprise-oriented project.

---

## 📂 Repository Structure

```

linux-system-security/
│
├── 01-user-and-permissions/
├── 02-ssh-hardening-and-access/
├── 03-system-enumeration/
├── 04-log-analysis
├── 05-intrusion-no-firewall/
├── 06-fail2ban-ssh-protection
└── 07-broken-sudoers

```

---

## 🧪 Lab Modules

### **Module 1 – User & Permissions Management**
- User creation  
- Group hierarchy  
- sudoers  
- passwd/shadow  
- permissions and ownership  
- basic access troubleshooting  

### **Module 2 – SSH Hardening & Access Control**
- Key-based authentication  
- sshd_config tuning  
- disabling password login  
- troubleshooting failed logins  
- log analysis (auth.log, journalctl)  

### **Module 3 – System Enumeration & Security Audit**
- SUID/SGID binaries  
- running processes  
- open ports (ss -tulnp)  
- services (systemctl)  
- filesystem inspection  
- kernel/system info  
- security posture analysis  

### **Module 4 - SSH Log Analysis**
- Identify invalid user access
- Detect brute-force user access
- Track root sudo activity
- Use `auth.log`, `journalctl`, and `last`
- Monitor SSH with system logs

### **Module 5 - SSH Intrusion + Firewall Misconfiguration**
- UFW firewall disabled simulation
- Nmap scan from attacker machine (Kali)
- SSH brute-force with hydra or manual testing
- Re-enable firewall and protect port 2222

### **Module 6 – SSH Brute-force Protection (fail2ban)**
- Simulate a brute-force attack from Kali (manual or hydra)
- Automatically block IP using fail2ban
- Analyze `/var/log/fail2ban.log` and `/var/log/auth.log`
- Unban a legitimate IP via `fail2ban-client`
- Learn fail2ban jail structure and reactive SSH defense

### **Module 7 – Broken sudoers configuration**
- Introduce a syntax error in `/etc/sudoers`
- Simulate total `sudo` access failure
- Test recovery methods via root or console
- Restore `sudo` with `visudo` safely

---

## 🎯 Goal of the Lab
To build a realistic, complete Linux security baseline similar to what is expected from Internal IT Engineers or Junior System Administrators.

The lab is designed to:
- Understand Linux deeply  
- Practice troubleshooting  
- Build a portfolio of technical scenarios  
- Prepare for professional interviews  

---

## 📌 Author
Part of my training to become an Internal IT Engineer in Japan.  
The structure and documentation follow professional standards used in enterprise environments.