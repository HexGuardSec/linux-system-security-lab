# SSH Hardening – HexGuard Server

## 1. Objective
Secure SSH access by disabling password login, limiting attempts, and enforcing key-based authentication.

---

## 2. Key Generation (Client Side)

Generate an ED25519 key pair for the user (example: Emilie):

```bash
ssh-keygen -t ed25519
````

* Public key: `~/.ssh/id_ed25519.pub`
* Private key: `~/.ssh/id_ed25519` (keep secret!)

---

## 3. Server Configuration

1. Copy the public key to the server:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub emilie@192.168.56.10
```

2. Harden SSH by editing `/etc/ssh/sshd_config`:

```text
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
LoginGraceTime 20
Protocol 2
X11Forwarding no
```

3. Check any additional `.d/` configs:

```bash
sudo grep -i password /etc/ssh/sshd_config.d/*.conf
```

* Ensure no file overrides `PasswordAuthentication no`

4. Restart SSH:

```bash
sudo systemctl restart ssh
```

---

## 4. Testing SSH Hardening

**Check that password login is blocked**:

```bash
ssh -o PubkeyAuthentication=no emilie@192.168.56.10 -v
```

* Expected result:

```
Permission denied (publickey,password)
```

* Connect with key:

```bash
ssh emilie@192.168.56.10
```

* Should succeed only with the authorized key.

---

## 5. Notes

* Keys are preferred over passwords for security.
* MaxAuthTries limits brute-force attempts.
* Always verify additional config files (`sshd_config.d`) for overrides.
* Keep private keys safe and do not share.