# Scenario 07 – Broken sudoers configuration

## 🎯 Objective

Simulate a real-world incident where the `/etc/sudoers` file is misconfigured, preventing all users from using `sudo`.  
Recover access and fix the configuration from a root shell or TTY session.

---

## 🧪 Lab Setup

- Ubuntu Server with user: `itadmin`
- SSH on port 2222
- User `itadmin` has full `sudo` privileges
- Fail2ban is active

---

## 🔹 Step 1 – Confirm `sudo` is working

Test as `itadmin`:

```bash
sudo whoami
# → root
````

📸 Screenshot: `01-sudo-ok-before-error.png`

---

## 🔹 Step 2 – Introduce a syntax error in `/etc/sudoers`

Using `visudo`:

```bash
sudo visudo
```

Append an invalid line:

```
BAD ENTRY WITHOUT PERMISSION
```

📸 Screenshot: `02-sudoers-modified.png`

---

## 🔹 Step 3 – Test the sudo failure

Open a new SSH session with `itadmin` and run:

```bash
sudo ls
```

Expected output:

```
>>> /etc/sudoers: syntax error near line XX <<<
sudo: parse error in /etc/sudoers
sudo: no valid sudoers sources found, quitting
```

📸 Screenshot: `03-sudo-broken.png`

---

## 🔹 Step 4 – Recover from root

Switch to `root` user (via TTY or existing session):

```bash
su -
visudo
```

Remove the invalid line and save.

📸 Screenshot: `04-sudo-restored.png`

---

## 🧠 Key Learnings

* How a small mistake in `sudoers` can lock out an entire system
* How to safely edit the sudoers file using `visudo`
* Why SSH + root access or console fallback is critical in real systems

---

## 📁 Files

* `scenario.md`
* `/screenshots/07-broken-sudoers/*.png`
