# 🔐 Linux Permission Management

Linux is a multi-user operating system, and **Permission Management** ensures that files and directories are accessed and modified only by authorized users. It is one of the most critical aspects of system security.

---

## 📌 What is Permission Management?

**Permission management** in Linux controls which users or groups can read, write, or execute files and directories. It helps ensure:

- Confidentiality (unauthorized users can’t read files)
- Integrity (unauthorized users can’t modify files)
- Controlled Execution (only authorized scripts/programs run)

---

## ❓ Why is Permission Management Important?

| Reason | Explanation |
|--------|-------------|
| 🔐 Security | Prevents unauthorized access and misuse of files or system resources |
| 👥 Multi-user Environment | Ensures each user accesses only what they are permitted |
| 📁 Data Integrity | Prevents unintentional overwriting or deletion |
| ⚙️ System Stability | Prevents scripts or processes from being executed improperly |

---

## ⚙️ Types of Permissions

Each file/directory in Linux has 3 types of permissions:

| Symbol | Meaning | Binary Value | Decimal |
|--------|---------|--------------|---------|
| `r`    | Read    | 100          | 4       |
| `w`    | Write   | 010          | 2       |
| `x`    | Execute | 001          | 1       |

Permissions are assigned to three types of users:

1. **User (u)** – Owner of the file
2. **Group (g)** – Group that owns the file
3. **Others (o)** – Everyone else

### Example:
```bash
-rwxr-xr--
### 🔢 Permission Breakdown Table
```
| **Section** | **Permission Symbols** | **Description**                      | **Numeric Value** |
|-------------|------------------------|--------------------------------------|-------------------|
| User        | `rwx`                  | Read, Write, Execute                 | 4 + 2 + 1 = **7** |
| Group       | `r-x`                  | Read, Execute                        | 4 + 0 + 1 = **5** |
| Others      | `r--`                  | Read only                            | 4 + 0 + 0 = **4** |

### Final Permission Example: `-rwxr-xr--`

| **User Type** | **Permissions** | **Numeric** |
|---------------|------------------|-------------|
| User (Owner)  | `rwx`            | 7           |
| Group         | `r-x`            | 5           |
| Others        | `r--`            | 4           |

**Total Octal Permission: `755`**
# 🔐 Linux Permission Management Guide

Manage your Linux file and directory permissions securely and efficiently using this comprehensive guide. Learn how to assign, modify, and control access using `chmod`, `chown`, `chgrp`, and more.

---

## 🔧 How to Manage Permissions

###  📄 View Permissions

```bash
ls -l filename
```
| **Commands**| **Description**  |
| --- | --- |
| chmod u+x filename  | Add execute permission to user|
|chmod g-w filename    |   # Remove write permission from group|
| chmod o=r filename   |    # Set read-only for others |

### 🔢 Numeric (Octal) Mode
| **Commands**| **Description**  |
| --- | --- |
|chmod 755 filename  |     rwx for user, rx for group and others|
|chmod 644 filename     |  rw for user, r for group and others|


### 📊 Common Permission Sets

| Octal | Access Level | User (Owner) | Group | Others | Symbolic |
|-------|---------------|--------------|-------|--------|----------|
| `777` | Full Access   | rwx          | rwx   | rwx    | `rwxrwxrwx` |
| `755` | Safe          | rwx          | r-x   | r-x    | `rwxr-xr-x` |
| `644` | Common        | rw-          | r--   | r--    | `rw-r--r--` |
| `700` | Private       | rwx          | ---   | ---    | `rwx------` |
| `600` | Confidential  | rw-          | ---   | ---    | `rw-------` |
| `775` | Group Writable| rwx          | rwx   | r-x    | `rwxrwxr-x` |

### 🗂️ Set Permissions for Directories
| **Commands**|
| --- | 
|chmod 755 <foldernam>|
|chmod -R 755 <foldername> |

### 🧪 Real-World Examples

| Command                             | Description                                      |
|-------------------------------------|--------------------------------------------------|
| `chmod 700 secrets.txt`            | Only owner has full access (private file)        |
| `chmod 644 public.txt`             | Owner can read/write, others can read            |
| `chmod 777 script.sh`              | Full access to everyone ⚠️ (not recommended)     |
| `chown saime file.txt`             | Change owner of file to `saime`                  |
| `chgrp devops file.txt`            | Change group ownership to `devops`               |
| `chmod -R 755 /home/saime/`        | Recursively give full access to owner, read-execute to others |
