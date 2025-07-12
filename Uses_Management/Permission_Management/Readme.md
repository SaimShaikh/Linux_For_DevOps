
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

| Icon | Symbol | Meaning | Binary Value | Decimal |
|------|--------|---------|--------------|---------|
| 📖   | `r`    | Read    | 100          | 4       |
| ✍️   | `w`    | Write   | 010          | 2       |
| 🏃  | `x`    | Execute | 001          | 1       |

Permissions are assigned to three types of users:

1.  **User (u)** – Owner of the file
2.  **Group (g)** – Group that owns the file
3.  **Others (o)** – Everyone else

### Example:

```bash
-rwxr-xr--
```

### 🔢 Permission Breakdown Table

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

---

## 🔧 How to Manage Permissions

###  📄 View Permissions

```bash
ls -l filename
```
The `ls -l` command displays detailed information about files and directories, including their permissions, owner, group, size, and modification date. The output format is as follows:

```
-rwxr-xr-- 1 user group 1024 Jul 12 13:00 filename
```

### ⚙️ Basic Commands

| **Commands** | **Description**                                  |
|--------------|--------------------------------------------------|
| `chmod u+x filename` | Add execute permission to user               |
| `chmod g-w filename` | Remove write permission from group             |
| `chmod o=r filename` | Set read-only for others                       |
| `chown user:group filename` | Change the owner and group of the file      |
| `chgrp groupname filename` | Change the group owner of the file           |

### 🔢 Numeric (Octal) Mode

| **Commands** | **Description**                                  |
|--------------|--------------------------------------------------|
| `chmod 755 filename` | `rwx` for user, `r-x` for group and others       |
| `chmod 644 filename` | `rw-` for user, `r--` for group and others       |
| `chmod 700 filename` | `rwx` for user, no permissions for group/others |
| `chmod 600 filename` | `rw-` for user, no permissions for group/others |

### 📊 Common Permission Sets

| Octal | Access Level   | User (Owner) | Group | Others | Symbolic    |
|-------|----------------|--------------|-------|--------|-------------|
| `777` | Full Access     | `rwx`        | `rwx` | `rwx`  | `rwxrwxrwx` |
| `755` | Safe           | `rwx`        | `r-x` | `r-x`  | `rwxr-xr-x` |
| `644` | Common         | `rw-`        | `r--` | `r--`  | `rw-r--r--` |
| `700` | Private        | `rwx`        | `---` | `---`  | `rwx------` |
| `600` | Confidential   | `rw-`        | `---` | `---`  | `rw-------` |
| `775` | Group Writable | `rwx`        | `rwx` | `r-x`  | `rwxrwxr-x` |

### 🗂️ Set Permissions for Directories

| **Commands**          | **Description**                                           |
|-----------------------|-----------------------------------------------------------|
| `chmod 755 <foldername>` | Sets permissions for a directory                         |
| `chmod -R 755 <foldername>`| Recursively sets permissions for all files/subdirectories |
| `chmod g+s <foldername>` | Set SGID bit on a directory so new files inherit group  |

### ➕ Special Permissions
Beyond the basic read, write, and execute permissions, Linux also supports special permissions:

*   **SUID (Set User ID):** When applied to an executable file, it runs with the permissions of the file owner rather than the user executing it. Set with: `chmod u+s filename` or `chmod 4xxx filename` (where xxx represents other permissions).
*   **SGID (Set Group ID):** When applied to an executable file, it runs with the permissions of the file group. When set on a directory, new files and subdirectories inherit the group ID of the directory. Set with: `chmod g+s directoryname` or `chmod 2xxx directoryname`.
*   **Sticky Bit:** When set on a directory, files within can only be deleted by their owners, the directory owner, or the root user. Set with: `chmod +t directoryname` or `chmod 1xxx directoryname`.

### 🧪 Real-World Examples

| Command                             | Description                                                      |
|-------------------------------------|------------------------------------------------------------------|
| `chmod 700 secrets.txt`            | Only owner has full access (private file)                        |
| `chmod 644 public.txt`             | Owner can read/write, others can read                            |
| `chmod 777 script.sh`              | Full access to everyone ⚠️ (not recommended)                     |
| `chown saime file.txt`             | Change owner of file to `saime`                                  |
| `chgrp devops file.txt`            | Change group ownership to `devops`                               |
| `chmod -R 755 /home/saime/public_html`| Recursively give full access to owner, read-execute to others for a website |
| `chmod +x script.sh`               | Adds execute permission for the owner                             |
| `chmod u+s executable`              | Sets the SUID bit on an executable                               |
| `chmod g+s directory`               | Sets the SGID bit on a directory                                |
| `chmod +t directory`                | Sets the sticky bit on a directory                              |

### ⛔ Common Permission Issues and Troubleshooting

| Issue                                  | Solution                                                                                             | Command(s) to Use                                                                 |
|----------------------------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| `Permission Denied` error              | Verify file permissions and ownership. Use `chmod` to modify permissions. Use `chown` to change ownership. | `ls -l`, `chmod`, `chown`                                                            |
| Script fails to execute                | Ensure the script has execute permissions for the appropriate users/groups.                     | `ls -l`, `chmod u+x script.sh`                                                      |
| Web server can't access files          | Ensure the web server user has necessary permissions to access files in the web directory.        | `chown -R www-data:www-data /var/www/html`, `chmod -R 755 /var/www/html`           |
| Cannot modify a file, even as owner     | Check if the file has write permissions for the owner.                                           | `ls -l`, `chmod u+w filename`                                                        |
| Insufficient disk space causing errors | Check available disk space.                                                                     | `df -h`                                                                           |

### 📚 Additional Commands

*   **`umask`**: Determines the default permissions for newly created files and directories.
    *   `umask` - displays the current umask value.
    *   `umask 022` - sets the umask so that new directories are created with 755 permissions and new files with 644 permissions.
*   **`id`**:  Find your user ID and group ID.
    *   `id` - Displays user ID, primary group ID, and list of supplementary group IDs.
    *   `id username` - Displays the ID information for a specific user.
*   **`groups`**: Find all groups to which you belong.
    *   `groups` - Lists all groups the current user is a member of.
    *   `groups username` - Lists all groups a specified user is a member of.
*   **`su`**: Switch to another user account.
    *   `su username` - Switch to the specified user. Requires the user's password.
*   **`sudo`**: Execute single commands with elevated privileges.
    *   `sudo command` - Executes the command as the superuser (root).

### ⚠️ Best Practices

*   **Least Privilege Principle:** Start with minimal permissions to ensure security.
*   **Use Groups:** Assign group permissions for efficient collaboration.
*   **Double-Check Recursive Commands:** Verify the impact of recursive commands to avoid unintended changes.
*   **Avoid `chmod 777`:** Refrain from using `chmod 777` unless absolutely necessary to avoid security risks.
*   **Set Execute Permissions on Scripts:** Ensure scripts have execute permission (`chmod +x`) to function correctly.
*   **Balance Permissions:** Avoid over-restricting files and directories, which can break application access.

---

## 📝 Assignment

### Scenario:

You are a system administrator for a small company. A new project requires a shared directory where developers can collaborate. The requirements are:

1.  A directory named `projectx` should be created in `/opt/`.
2.  A group named `developers` should own the directory.
3.  Only members of the `developers` group should be able to create, modify, and delete files in the directory.
4.  Other users should not have any access to the directory.

### Tasks:

1.  Create the `developers` group.
2.  Create the `projectx` directory in `/opt/`.
3.  Change the group ownership of the `projectx` directory to `developers`.
4.  Set the appropriate permissions on the `projectx` directory to meet the requirements.
5.  Verify the permissions and ownership of the directory.

### Bonus Task:
Ensure that all new files and directories created inside `projectx` automatically inherit the `developers` group.

### Commands to Use:

*   `groupadd`
*   `mkdir`
*   `chgrp`
*   `chmod`
*   `ls -l`
