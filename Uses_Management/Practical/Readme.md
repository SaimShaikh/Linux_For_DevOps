# 👨‍💻 Linux User & Group Management Practical Guide

This practical guide covers **essential Linux commands** for managing users, groups, passwords, and group administration. It also explains how to switch users and manage permissions.

---

## 📁 Table of Contents

- [View Existing Users & Groups](#view-existing-users--groups)
- [Add & Manage Users](#add--manage-users)
- [Modify User Information (`-c`, etc.)](#modify-user-information)
- [Password Management & Lock/Unlock (`-L`, `-U`)](#password-management--lockunlock)
- [Password Policies & Expiry](#password-policies--expiry)
- [Switch Users](#switch-users)
- [Group Management](#group-management)
- [Manage Group Membership (`gpasswd -a`, -d, -m, -A)](#manage-group-membership)
- [Bonus: Finger Command Setup](#bonus-finger-command-setup)

---

## 🔍 View Existing Users & Groups

| Command                            | Purpose                                 |
|------------------------------------|-----------------------------------------|
| `cat /etc/passwd`                  | List all users                          |
| `cut -d: -f1 /etc/passwd`          | List only usernames                     |
| `getent passwd`                    | Show users from system database         |
| `getent group`                     | Show all groups                         |
| `getent group groupname`           | Show a particular group's members       |

---

## ➕ Add & Manage Users

| Command                                     | Purpose                                  |
|---------------------------------------------|------------------------------------------|
| `sudo useradd saime`                        | Create user without home directory       |
| `sudo useradd -m john`                      | Create user with home directory          |
| `sudo passwd saime`                         | Set password for user                    |
| `id saime`                                  | Show user ID and group info              |
| `sudo usermod -aG docker saime`             | Add user to an additional group          |
| `sudo userdel saime`                        | Delete user                              |
| `sudo userdel -r saime`                     | Delete user and remove home directory    |

---

## ✏️ Modify User Information

| Command                                    | Purpose                                   |
|--------------------------------------------|-------------------------------------------|
| `sudo usermod -c "DevOps Engineer" saime`  | Add comment to user (seen in `finger`)    |

---

## 🔐 Password Management & Lock/Unlock

| Command                        | Purpose                               |
|---------------------------------|---------------------------------------|
| `sudo passwd -l saime`          | Lock user password (`-L` alternative) |
| `sudo passwd -u saime`          | Unlock user password (`-U` alternative) |
| `sudo usermod -L saime`         | Lock user account                     |
| `sudo usermod -U saime`         | Unlock user account                   |

---

## 🗕️ Password Policies & Expiry

| Command                                | Purpose                                 |
|----------------------------------------|-----------------------------------------|
| `sudo chage -l saime`                  | Show password expiry info               |
| `sudo chage -M 90 saime`               | Set password expiry to 90 days          |
| `sudo chage -W 7 saime`                | Warn user 7 days before expiry          |
| `sudo chage -I 7 saime`                | command is used to manage password aging policies for a user. -I <days> → Specifies the number of inactive days after a password expires before the account is permanently disabled.|

Example `chage -l saime` output:

```
Last password change                                    : Jul 09, 2025
Password expires                                        : Oct 07, 2025
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 1
Maximum number of days between password change          : 90
Number of days of warning before password expires       : 7
```

---

## 🔄 Switch Users

| Command                | Purpose                                   |
|------------------------|-------------------------------------------|
| `su - saime`           | Switch to user `saime` (password needed if not root) |
| `sudo su - saime`      | Switch to user without password (root only) |
| `whoami`               | Show current user                         |
| `exit`                 | Exit back to previous user                |

---

## 👥 Group Management

| Command                                | Purpose                             |
|----------------------------------------|-------------------------------------|
| `sudo groupadd developers`             | Create new group                    |
| `sudo groupdel developers`             | Delete a group                      |

---

## 🔧 Manage Group Membership

### ➕ Add a User to a Group
```bash
sudo gpasswd -a saime developers
```

### ➖ Remove a User from a Group
```bash
sudo gpasswd -d saime developers
```

### ✏️ Replace All Group Members (`-m`)
```bash
sudo gpasswd -m saime,john developers
```

### ⚙️ Manage Group Admins (`-A`)
```bash
sudo gpasswd -A saime developers
```

### 🔍 Example `/etc/group` Entry
```
developers:x:1003:saime,john
```
### 👤 comment user 
``` bash 
usermod -c "Your comment here" <username>
```
### Output
<img width="759" alt="Screenshot 2025-07-10 at 1 03 57 PM" src="https://github.com/user-attachments/assets/1c9ba4b8-983f-4b1b-854e-aa94e2978bbd" />


### ❌ This command changes the shell of user saime to /sbin/nologin, preventing them from accessing the system via SSH or the terminal.
``` bash 
usermod -s /sbin/nologin saime
```
### ✅ Allow for login 
``` bash 
usermod -s /bin/bash <username>
```
---

## 📂 View Group Members
```bash
getent group developers
```

Example output:
```
developers:x:1003:saime,john
```

---

## 🎯 Group Admin vs Members

| Option | Purpose                          | Example                                    |
|-------|----------------------------------|------------------------------------------|
| `-a`  | Add a single user                | `sudo gpasswd -a user group`              |
| `-d`  | Delete a user                    | `sudo gpasswd -d user group`              |
| `-m`  | Replace group members            | `sudo gpasswd -m user1,user2 group`       |
| `-A`  | Set group admins                 | `sudo gpasswd -A admin1,admin2 group`     |
| `-c`  | comment the user                 | `sudo usermod -c "your comment" <username>`|

---

## 🌟 Example Practical Flow:

```bash
# Create users
sudo useradd -m saime
sudo useradd -m john
sudo passwd saime
sudo passwd john

# Create group and add users
sudo groupadd devteam
sudo gpasswd -a saime devteam
sudo gpasswd -a john devteam

# Set group admins
sudo gpasswd -A saime devteam

# Check group info
getent group devteam

# Lock and unlock users
sudo usermod -L saime
sudo usermod -U saime
```

---

## 🏱️ Bonus: Finger Command Setup

### ➕ Install finger
```bash
sudo apt install finger   # Debian/Ubuntu
sudo yum install finger   # RedHat/CentOS
```

### 🔍 Use finger
```bash
finger saime
```
<img width="615" alt="Screenshot 2025-07-09 at 9 05 20 PM" src="https://github.com/user-attachments/assets/ece66bbe-0402-44e7-b8d8-a42b38c5679b" />


### ✏️ Set user comment (full name or you can write anything )
```bash
sudo usermod -c "Saime Shaikh - DevOps Engineer" saime
```

---

## ⚠️ Important Files

| File            | Purpose                                |
|-----------------|----------------------------------------|
| `/etc/passwd`   | Basic user information                |
| `/etc/shadow`   | Encrypted user passwords              |
| `/etc/group`    | Group information                     |
| `/etc/login.defs` | Default password policies            |

---

✅ **Practice Tip:**  
After each command, verify results using:
```bash
cat /etc/passwd
cat /etc/shadow
cat /etc/group

