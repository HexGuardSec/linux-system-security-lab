# Scenario 05 – SSH Intrusion with Firewall Disabled

## 🎯 Objective

Simulate a common misconfiguration in production environments where a server runs with an open SSH port and no active firewall.  
Demonstrate how an attacker can discover and target the machine, and how to analyze the resulting logs.

---

## 🛠️ Lab Setup

- Ubuntu Server with SSH listening on port `2222`
- UFW firewall **disabled**
- Kali Linux used to simulate external attacker
- Fail2ban temporarily disabled to allow brute-force simulation

---

## 🔹 Step 1 – Disable UFW (Firewall)

Command:
```bash
sudo ufw disable
````

Purpose:

* Simulate a misconfigured server left unprotected

📸 Screenshot: `01-ufw-disabled.png`

---

## 🔹 Step 2 – External Nmap Scan

From Kali machine:

```bash
nmap -p 2222 192.168.56.106
```

Purpose:

* Detect open SSH port

📸 Screenshot: `02-nmap-scan.png`

---

## 🔹 Step 3 – SSH Brute-Force Attack

Manual:

```bash
ssh staffuser@192.168.56.106 -p 2222
# Enter wrong password multiple times
```

Or with Hydra:

```bash
hydra -l staffuser -P worldlist.txt ssh://192.168.56.106:2222
```

Purpose:

* Simulate attack behavior and generate logs

📸 Screenshot: `03-ssh-bruteforce.png`

---

## 🔹 Step 4 – Analyze Authentication Logs

On Ubuntu server:

```bash
sudo tail -n 50 /var/log/auth.log
sudo journalctl -u ssh
```

Purpose:

* Review failed login logs and attacker footprint

📸 Screenshot: `04-authlog-brute.png`

---

## 🔹 Step 5 – Re-enable Firewall with Correct Rule

Restore minimal protection:

```bash
sudo ufw enable
sudo ufw allow 2222/tcp
```

Verify:

```bash
sudo ufw status numbered
```

📸 Screenshot: `05-ufw-reenabled.png`

---

## 🧠 Key Learnings

* Importance of default firewall configuration
* Detection of brute-force attempts via logs
* Difference between scanned vs. firewalled hosts
* SSH behavior with and without fail2ban
* Simple log-based intrusion monitoring

---

## 📁 Files

* Screenshots: `/05-intrusion-no-firewall/screenshots/`

---

## 🔒 Notes

* Fail2ban was disabled to simulate brute-force behavior
* Nmap used only to detect SSH port (not exploit)