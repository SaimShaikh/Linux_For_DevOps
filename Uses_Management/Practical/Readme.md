# 👨‍💻 Linux User & Group Management Practical Guide

This practical guide covers **essential Linux commands** for managing users, groups, passwords, and account policies. Each section is organized clearly for ease of understanding and practice.

---

## 📁 Table of Contents

- [User Management](#-user-management)
  - [View Existing Users](#-view-existing-users)
  - [Add Users](#-add-users)
  - [Modify User Information](#️-modify-user-information)
  - [Password Management](#-password-management)
  - [Password Expiry & Policies](#️-password-expiry--policies)
  - [Switch Between Users](#️-switch-between-users)
  - [Special User Shells](#️-special-user-shells)
  - [Bonus: Finger Command Setup](#-bonus-finger-command-setup)
- [Group Management](#-group-management)
  - [View Existing Groups](#-view-existing-groups)
  - [Create & Delete Groups](#-create--delete-groups)
  - [Manage Group Membership](#-manage-group-membership)
  - [Group Admins vs Members](#️-group-admins-vs-members)
- [Key System Files](#-key-system-files)
- [Example Practical Flow](#️-example-practical-flow)

---

# 🔑 User Management

---

## 🔍 View Existing Users

| Command                   | Purpose                            |
|---------------------------|------------------------------------|
| `cat /etc/passwd`         | List all users                     |
| `cut -d: -f1 /etc/passwd` | List only usernames                |
| `getent passwd`           | Show users from system database    |

---

## ➕ Add Users

| Command                             | Purpose                                |
|--------------------------------------|----------------------------------------|
| `sudo useradd saime`                 | Create user (no home directory)        |
| `sudo useradd -m john`               | Create user with home directory        |
| `sudo passwd saime`                  | Set user password                      |
| `sudo userdel saime`                 | Delete user                            |
| `sudo userdel -r saime`              | Delete user and remove home directory  |
| `id saime`                           | Show user ID and groups                |
| `sudo usermod -u 3000 saime`         | Change user ID                         |
| `sudo usermod -c "DevOps Engineer" saime` | Add a comment (seen in finger) |

---

## ✏️ Modify User Information

| Command                                     | Purpose                            |
|---------------------------------------------|------------------------------------|
| `sudo usermod -c "DevOps Engineer" saime`   | Add or modify comment for user     |
| `sudo usermod -s /sbin/nologin saime`       | Disable shell access               |
| `sudo usermod -s /bin/bash saime`           | Enable shell access (default bash) |

---

## 🔐 Password Management

| Command                        | Purpose                               |
|---------------------------------|---------------------------------------|
| `sudo passwd -l saime`          | Lock user password                    |
| `sudo passwd -u saime`          | Unlock user password                  |
| `sudo usermod -L saime`         | Lock user account                     |
| `sudo usermod -U saime`         | Unlock user account                   |

---

## 🗕️ Password Expiry & Policies

| Command                           | Purpose                               |
|------------------------------------|---------------------------------------|
| `sudo chage -l saime`              | List password expiry details          |
| `sudo chage -M 90 saime`           | Set max password age to 90 days       |
| `sudo chage -m 9 saime`            | Set min password age to 9 days        |
| `sudo chage -W 7 saime`            | Warn user 7 days before expiry        |
| `sudo chage -I 7 saime`            | Lock inactive accounts after 7 days   |

Example Output:

Last password change : Jul 09, 2025
Password expires : Oct 07, 2025
Password inactive : never
Account expires : never
Minimum number of days between password change : 1
Maximum number of days between password change : 90
Number of days of warning before password expires : 7


---

## 🔄 Switch Between Users

| Command              | Purpose                                    |
|----------------------|--------------------------------------------|
| `su - saime`         | Switch user (asks for password)           |
| `sudo su - saime`    | Switch user as root (no password needed) |
| `whoami`             | Show current user                          |
| `exit`               | Return to previous user                   |

---

## 🚫 Special User Shells

| Command                                      | Purpose                           |
|----------------------------------------------|-----------------------------------|
| `sudo usermod -s /sbin/nologin saime`        | Disable terminal & SSH access     |
| `sudo usermod -s /bin/bash saime`            | Enable terminal access            |

---

## 🏱️ Bonus: Finger Command Setup

Install `finger` command:
```bash
sudo apt install finger       # Debian/Ubuntu
sudo yum install finger       # RedHat/CentOS
```
### finger saime
``` bash
finger saime
```
<img width="615" height="102" alt="Screenshot 2025-07-09 at 9 05 20 PM" src="https://github.com/user-attachments/assets/3715e267-f211-4e61-8dfa-1589b52407e5" />

# 👥 Group Management

---

## 🔍 View Existing Groups

| Command                    | Purpose                          |
|----------------------------|----------------------------------|
| `getent group`             | Show all groups                  |
| `getent group groupname`   | Show members of a specific group |
| `cat /etc/group`           | Manually view group file         |

---

## ➕ Create & Delete Groups

| Command                        | Purpose                      |
|---------------------------------|------------------------------|
| `sudo groupadd developers`     | Create new group             |
| `sudo groupdel developers`     | Delete a group               |
| `sudo gpasswd developers`      | Assign password to the group |

Verify group password in `/etc/gshadow`:
```bash
sudo cat /etc/gshadow
```
## 🔧 Manage Group Membership

| Command                                      | Purpose                    |
|----------------------------------------------|----------------------------|
| `sudo gpasswd -a saime developers`           | Add user to a group        |
| `sudo gpasswd -d saime developers`           | Remove user from a group   |
| `sudo gpasswd -m saime,john developers`      | Replace all group members  |
| `sudo gpasswd -A saime developers`           | Set group admin            |

### 🔍 View Group Members

```bash
getent group developers
```
### Example output
``` bash
developers:x:1003:saime,john
```
## 🎯 Group Admins vs Members

| Option | Purpose                  | Example Command                     |
|-------|---------------------------|--------------------------------------|
| `-a`  | Add a single user         | `sudo gpasswd -a user group`         |
| `-d`  | Remove a single user      | `sudo gpasswd -d user group`         |
| `-m`  | Replace group members     | `sudo gpasswd -m user1,user2 group` |
| `-A`  | Set group admins          | `sudo gpasswd -A admin1 group`      |

## ⚠️ Key System Files

| File               | Purpose                              |
|--------------------|--------------------------------------|
| `/etc/passwd`      | Basic user account information      |
| `/etc/shadow`      | Encrypted user passwords            |
| `/etc/group`       | Group membership information        |
| `/etc/gshadow`     | Secure group passwords & admins    |
| `/etc/login.defs`  | Default password & login policies   |
