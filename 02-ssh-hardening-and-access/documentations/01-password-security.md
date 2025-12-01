# Linux Password Security – Technical Overview

## 1. Purpose
This document explains how Linux manages user authentication through the `/etc/passwd` and `/etc/shadow` files, how password hashing works, and how account locking and aging policies are applied.  

---

## 2. `/etc/passwd` – User Information (Non-Sensitive)

The `/etc/passwd` file stores basic user account information.  
It is readable by all users and does **not** contain password hashes.

Example entry:

```

emilie:x:1001:1001::/home/emilie:/bin/bash

```

### Field explanation
| Field | Description |
|-------|-------------|
| 1     | Username |
| 2     | `x` → placeholder indicating password is stored in `/etc/shadow` |
| 3     | UID (User ID) |
| 4     | GID (Primary Group ID) |
| 5     | Comment / GECOS |
| 6     | Home directory |
| 7     | Login shell |

---

## 3. `/etc/shadow` – Password Hashes and Aging Policies

The `/etc/shadow` file stores **password hashes and expiration rules**.  
Only root can read it.

Example entry:

```

emilie:$6$kHGowQJp...:19842:0:99999:7:::

```

### Field explanation
| Field | Description                                  |
|-------|----------------------------------------------|
| 1     | Username                                     |
| 2     | Password hash (`$6$` = SHA-512)              |
| 3     | Days since last password change (epoch days) |
| 4     | Minimum days before password can be changed  |
| 5     | Maximum days before password expires         |
| 6     | Warning period before expiration             |
| 7     | Inactive days after expiration               |
| 8     | Account expiration date                      |
| 9     | Reserved                                     |

---

## 4. Password Locking / Unlocking

### Lock an account
```

sudo passwd -l paul

```
This adds a `!` in front of the hash in `/etc/shadow`, preventing authentication.

### Unlock an account
```

sudo passwd -u paul

```
This removes the `!`.

### Delete a password (no authentication required)
```

sudo passwd -d paul

```

---

## 5. Checking Password Aging Policies

To display ageing data:
```

sudo chage -l paul

```

Example output:

```

Last password change : Feb 25, 2025
Password expires     : never
Password inactive    : never
Minimum number of days between password change : 0
Maximum number of days between password change : 99999
Number of days of warning before password expires : 7

```

---

## 6. Key Takeaways

- `/etc/passwd` → contains user info, publicly readable.
- `/etc/shadow` → contains password hashes + expiration rules, root-only.
- `$6$` prefix → means the hash uses SHA-512.
- Locked accounts show `!` before the hash.
- `chage` is used to inspect and manage password aging policies.

---

## 7. Practical Commands Used

```

cat /etc/passwd
sudo cat /etc/shadow
sudo passwd -l user
sudo passwd -u user
sudo passwd -d user
sudo chage -l user

```