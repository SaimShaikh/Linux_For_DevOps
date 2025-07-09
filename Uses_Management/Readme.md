\# 👥 Linux User Management

## 📌 What is User Management?

User management in Linux refers to the process of **creating, modifying, deleting, and managing users and groups** within the system.  
It ensures that **multiple users can securely access and operate the same system without interfering with each other’s data or operations.**

---

## 🔍 Why Do We Need User Management in Linux?

- ➡️ **Multi-user Environment:** Linux is a multi-user operating system. Managing users helps maintain order and security.
- ➡️ **Access Control:** Assign appropriate permissions to different users to prevent unauthorized actions.
- ➡️ **Resource Management:** Allocate resources fairly among users.
- ➡️ **System Security:** Keep the system secure by limiting what each user can do.

---

## 👤 Types of Users in Linux

| Type of User            | Description                                                         |
|-------------------------|---------------------------------------------------------------------|
| **Root User 👑**        | The administrator of the system. Full control over everything. Also called **superuser**. |
| **Normal User 🙂**      | Created by admin or during OS installation. Limited permissions for safety. |
| **System/User Services 🛡️** | Service accounts used by system processes (like `www-data`, `mysql`, etc.). |

---

## ⚖️ Normal User vs Admin User (Root)

| Feature/Capability             | Normal User 🙂         | Admin User 👑 (Root/Sudo) |
|---------------------------------|------------------------|--------------------------|
| Privileges                      | Limited                | Full                     |
| Can install software            | ❌                     | ✅                        |
| Modify system files             | ❌                     | ✅                        |
| Create/delete users              | ❌                     | ✅                        |
| Uses `sudo` for admin tasks     | ✅ (If allowed)        | Not Required             |
| Home directory                  | `/home/username`       | `/root`                  |
| UID Range                       | 1000+                  | 0                        |

---

## 🔧 Important User & Group Commands

### ➕ User Management Commands

| Command          | Description                     | Example                       |
|------------------|---------------------------------|-------------------------------|
| `useradd`        | Add a new user                  | `sudo useradd john`           |
| `adduser`        | Interactive user creation       | `sudo adduser john`           |
| `passwd`         | Set/change user password        | `sudo passwd john`            |
| `usermod`        | Modify an existing user         | `sudo usermod -aG sudo john`  |
| `userdel`        | Delete a user                   | `sudo userdel john`           |

---

### 👥 Group Management Commands

| Command          | Description                     | Example                           |
|------------------|---------------------------------|-----------------------------------|
| `groupadd`       | Create a group                  | `sudo groupadd developers`        |
| `gpasswd`        | Add user to a group             | `sudo gpasswd -a john developers` |
| `groups`         | Show groups of a user           | `groups john`                      |
| `groupdel`       | Delete a group                  | `sudo groupdel developers`         |

---

### 📂 Important Files

| File            | Purpose                          | Example View          |
|-----------------|----------------------------------|-----------------------|
| `/etc/passwd`   | Contains user account info       | `cat /etc/passwd`     |
| `/etc/group`    | Contains group info              | `cat /etc/group`      |
| `/etc/shadow`   | Contains encrypted passwords     | `sudo cat /etc/shadow`|

#### Example of `/etc/passwd` entry:
#### `tail -n <number> /etc/passwd` to check user is created or not after that you can see the your user name which user created 
#### `/etc/shadow` or `tail -1 /etc/shadow` in this place where user password is stored as a normal user we can’t assess this location  


**Explanation:**
- `john` → Username
- `x` → Password placeholder (real password is in `/etc/shadow`)
- `1001` → User ID (UID)
- `1001` → Group ID (GID)
- `John Doe` → User description
- `/home/john` → Home directory
- `/bin/bash` → Default shell

---

## 🔄 Switching Between Users

| Action                          | Command                     | Example                |
|----------------------------------|-----------------------------|------------------------|
| Switch user                      | `su - username`             | `su - john`            |
| Login as root                    | `sudo -i`                   | `sudo -i`              |
| Exit user session                | `exit`                      | `exit`                 |
| Execute command as another user  | `sudo -u username command`  | `sudo -u john whoami`  |

---
##⚙️ Common Options
## 📊 Tables

|  Option  | Description|
| --- | --- |
| -a|  Add a user to the group |
| -d|  Delete a user from the group |
| -m|  Set multiple users as the group's members (replaces current list)|

## ✅ Practical Example

```bash
# Create a user named alice
sudo adduser alice  

# Add alice to the sudoers group
sudo usermod -aG sudo alice  

# Set a password for alice
sudo passwd alice  

# Switch to alice's account
su - alice  

# Check alice's groups
groups
