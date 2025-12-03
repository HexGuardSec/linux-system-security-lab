## 📝 `09-critical-file-tampering.md` — version finale

````markdown
# Scenario 09 – Critical File Tampering

🎯 **Objective**  
Simulate a case where a misconfigured user (`maluser`) edits `/etc/passwd`, causing login or privilege issues on the system.

---

## 🧩 Context

A system administrator accidentally adds a regular user (`maluser`) to the `sudo` group.  
The user gains privileged access and modifies `/etc/passwd`, either breaking another user account or altering shell configuration.  
This simulates a common misconfiguration or insider misuse found in real IT environments.

---

## 🛠️ Steps to Reproduce

### 1. Create a new user
```bash
sudo adduser maluser
````

### 2. Add the user to `sudo` group

```bash
sudo usermod -aG sudo maluser
```

### 3. Switch to maluser and edit `/etc/passwd`

```bash
su - maluser
sudo nano /etc/passwd
```

⚠️ Modified `staffuser`'s shell path to an invalid value (`/bin/garbage`)
or broke their line syntax.

### 4. Attempt to switch to `staffuser`

```bash
su - staffuser
```

Expected: login failure due to invalid shell.

### 5. Analyze logs for root cause

```bash
sudo journalctl -xe
sudo tail -n 50 /var/log/auth.log
```

### 6. Restore the correct `/etc/passwd` entry

Fix `staffuser`'s shell path or re-add the missing line.

### 7. Cleanup

```bash
sudo kill -9 <maluser_pid>   # if necessary
sudo deluser --remove-home maluser
```

---

## 📄 Logs Observed

Sample entries:

```log
su: No shell: /bin/garbage
userdel: user maluser is currently used by process 1450
```

---

## 🔐 Lessons Learned

* Never assign `sudo` rights without validation
* Know how to recover from `/etc/passwd` corruption
* Always check for login shell correctness
* Critical files require strict ownership and controlled access

---

## 📸 Screenshots

| Filename                          | Description                            |
| --------------------------------- | -------------------------------------- |
| `01-adduser-maluser`              | Created test user                      |
| `02-add-maluser-group-sudo`       | Gave `maluser` sudo rights             |
| `03-passwd-modify`                | Edited `/etc/passwd` with broken shell |
| `04-error-connection-staffuser`   | Connection error with broken account   |
| `05-journalctl-connection-denied` | Log showing connection issues          |
| `06-repare-passwd`                | File restored correctly                |
| `07-connection-staffuser-ok`      | Successful login after repair          |
| `08-delete-malicious-user`        | `maluser` deleted from the system      |