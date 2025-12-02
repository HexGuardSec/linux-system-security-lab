# Scenario 06 – SSH Brute-Force Protection with fail2ban

## 🎯 Objective

Simulate an SSH brute-force attack from an external host and demonstrate how `fail2ban` automatically detects and bans the attacker’s IP after multiple failed login attempts.

---

## 🧪 Lab Setup

- Ubuntu Server with SSH on port `2222`
- Kali Linux used to simulate brute-force attempts
- Fail2ban installed and SSH jail enabled
- SSH password authentication temporarily allowed
- Port 2222 exposed in `ufw`

---

## 🔹 Step 1 – Verify fail2ban configuration

Ensure fail2ban is running and SSH jail is active:
```bash
sudo systemctl status fail2ban
sudo fail2ban-client status sshd
````

Check configuration (example):

```ini
[sshd]
enabled = true
port = 2222
```

Restart fail2ban:

```bash
sudo systemctl restart fail2ban
```

📸 Screenshot: `01-fail2ban-status.png`

---

## 🔹 Step 2 – Simulate Brute-force Attack

From Kali:

**Option A – Hydra:**

```bash
hydra -l guestuser -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.106:2222
```

**Option B – Manual:**

```bash
ssh guestuser@192.168.56.106 -p 2222
# Enter incorrect password multiple times
```

📸 Screenshot: `02-bruteforce-attack.png`

---

## 🔹 Step 3 – fail2ban Blocks the IP

SSH attempts from Kali now show:

```bash
ssh: connect to host 192.168.56.106 port 2222: Connection refused
```

Check jail status:

```bash
sudo fail2ban-client status sshd
```

📸 Screenshot: `03-banned-logs.png`

---

## 🔹 Step 4 – Analyze Logs

Check ban details:

```bash
sudo tail -n 20 /var/log/fail2ban.log
```

📸 Screenshot: `04-fail2ban-log.png`

---

## 🔹 Step 5 – Unban the IP

To manually unblock Kali’s IP:

```bash
sudo fail2ban-client set sshd unbanip 192.168.56.107
```

📸 Screenshot: `05-unban-ip.png`

---

## 🧠 Key Learnings

* How fail2ban detects SSH brute-force attacks
* Jail structure and log monitoring
* Reactive defense in real-time
* Understanding the difference between auth.log and fail2ban.log

---

## 📁 Files

* `scenario.md`
* `/screenshots/06-fail2ban-ssh-protection/*.png`