# 🔍 Scenario 10 — Unknown Port / Hidden Service Detection

## 🎯 Objective

Simulate a real-world situation where an unknown open port is discovered on a production system.  
The goal is to identify the process responsible, analyze its legitimacy, and take corrective action.

---

## 🖥️ Environment

- OS: Ubuntu Server 24.04  
- Role: Internal IT Engineer  
- Tools: `ss`, `netstat`, `systemctl`, `ps`, `lsof`, `nc`

---

## 🧪 Step-by-step Procedure

### ✅ Step 1 — List Running Services

Check all actively running services:

```bash
systemctl list-units --type=service
````

📸 `01-services-running.png`

---

### ✅ Step 2 — List Enabled Services at Boot

List services set to launch automatically:

```bash
systemctl list-unit-files --type=service | grep enabled
```

📸 `02-services-enabled.png`

---

### ✅ Step 3 — Check Root-owned Processes

Display all processes owned by the `root` user:

```bash
ps -U root -u root u
```

📸 `03-processes-root.png`

---

### ✅ Step 4 — Verify Critical Services

Inspect SSH and cron status:

```bash
systemctl status ssh
systemctl status cron
```

📸 `04-status-ssh-cron.png`

---

### ✅ Step 5 — Enumerate Open Ports

Identify listening ports and their associated processes:

```bash
sudo ss -tulnp
```

📸 `05-ss-tulnp.png`

Alternative:

```bash
sudo netstat -tulpen
```

📸 `06-netstat-tulpen.png`

---

### ✅ Step 6 — Simulate an Unknown Port (Netcat)

Simulate a suspicious service on port `7777`:

**On the server:**

```bash
sudo nc -lvnp 7777
```

**From Kali:**

```bash
nc 192.168.56.106 7777
```

📸 `09-nc-connection-kali.png`

---

## ✅ Conclusion

This scenario demonstrates how to:

* Detect unknown open ports
* Cross-check with services and processes
* Simulate real-world threats with tools like Netcat
* Investigate suspicious services

---

## 🧠 Key Takeaways

* An open port should always be explainable.
* Unexpected listeners are a red flag for potential misconfigurations or compromise.
* Use `ss`, `ps`, `netstat`, and `systemctl` together for deep enumeration.

---

## 📁 Screenshots

* `01-services-running.png`
* `02-services-enabled.png`
* `03-processes-root.png`
* `04-status-ssh-cron.png`
* `05-ss-tulnp.png`
* `06-netstat-tulpen.png`
* `09-nc-connection-kali.png`