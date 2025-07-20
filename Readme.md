
# 🐧 Linux Command Cheat Sheet

A comprehensive list of essential Linux commands with concise explanations — perfect for beginners, sysadmins, DevOps engineers, and cloud learners.

---

## 📂 File & Directory Management

| Command | Description |
|--------|-------------|
| `ls` | List directory contents |
| `ls -l` | Long listing format |
| `ll <file name >` | list the permission of specific file  |
| `lsblk` | Linux is used to list block devices |
| `ls -a` | List all files including hidden |
| `cd <dir>` | Change directory |
| `cmp <file1> <file2>` | compare both files  |
| `diff <file1> <file2>` | find the difference between  both files  |
| `pwd` | Print working directory |
| `mkdir <dir>` | Create a directory |
| `touch <file>` | Create an empty file |
| `rm <file>` | Remove a file |
| `rm -rvf <dir>` | Remove directory forcefully  |
| `rm -r <dir>` | Remove directory recursively |
| `cp <src> <dest>` | Copy files or directories |
| `mv <src> <dest>` | Move or rename files/directories |
| `find <path> -name "<pattern>"` | Find files by name |

---

## 📄 Viewing File Content

| Command | Description |
|--------|-------------|
| `cat <file>` | Display file content |
| `tree <file>` | Display file starture  |
| `tac <file>` | Display content in reverse |
| `more <file>` | View file one page at a time |
| `less <file>` | Scrollable file viewer |
| `head <file>` | First 10 lines of a file |
| `tail <file>` | Last 10 lines of a file |
| `tail -f <file>` | Live monitoring (e.g. logs) |

---

## 🔍 Searching & Sorting

| Command | Description |
|--------|-------------|
| `grep "text" <file>` | Search for text in file |
| `egrep 'pattern ' <file>` | Search using extended regular expressions |
| `grep -r "text" <dir>` | Recursive search |
| `sort <file>` | Sort lines in a file |
| `uniq <file>` | Remove duplicates |
| `wc -l <file>` | Count lines in file |
| `cut -d':' -f1 <file>` | Cut by delimiter |
| `awk '{print $1}' <file>` | Print first column |
| `sed 's/old/new/g' <file>` | Replace text |

---

## 🧑‍💻 User & Group Management

| Command | Description |
|--------|-------------|
| `whoami` | Show current user |
| `id` | User ID and group info |
| `adduser <user>` | Add new user |
| `passwd <user>` | Set user password |
| `deluser <user>` | Delete user |
| `groupadd <group>` | Add new group |
| `usermod -aG <group> <user>` | Add user to group |
| `groups <user>` | Show user's groups |

---

## 🔐 Permissions & Ownership

| Command | Description |
|--------|-------------|
| `chmod 755 <file>` | Change file permissions |
| `chown user:group <file>` | Change file owner |
| `umask` | Default permission mask |
| `ls -l` | Show permissions |

---

## 🧪 Process Management

| Command | Description |
|--------|-------------|
| `ps aux` | Show all processes |
| `top` | Real-time process viewer |
| `htop` | Interactive process viewer (needs install) |
| `kill <PID>` | Kill a process |
| `killall <name>` | Kill all by name |
| `bg` / `fg` | Background/foreground job control |
| `nice -n <value> <command>` | Set process priority |

---

## 🌐 Networking

| Command | Description |
|--------|-------------|
| `ip a` / `ifconfig` | Show IP addresses |
| `ping <host>` | Ping remote host |
| `traceroute <host>` | Route to host |
| `nslookup <host>` | DNS lookup |
| `dig <host>` | Detailed DNS query |
| `netstat -tulnp` | Show ports & connections |
| `ss -tuln` | Show listening ports |
| `wget <url>` | Download from web |
| `curl <url>` | Fetch from URL |

---

## 📦 Package Management (Debian-based)

| Command | Description |
|--------|-------------|
| `apt update` | Update package list |
| `apt upgrade` | Upgrade packages |
| `apt install <pkg>` | Install a package |
| `apt remove <pkg>` | Remove a package |
| `dpkg -i <file.deb>` | Install .deb package |
| `apt-cache search <pkg>` | Search package |

---

## 🗄 Compression & Archives

| Command | Description |
|--------|-------------|
| `tar -cvf file.tar <dir>` | Create tarball |
| `tar -xvf file.tar` | Extract tarball |
| `gzip <file>` | Compress a file |
| `gunzip <file.gz>` | Decompress |
| `zip <file.zip> <file>` | Create zip file |
| `unzip <file.zip>` | Extract zip file |

---

## 🔄 Disk & System Info

| Command | Description |
|--------|-------------|
| `df -h` | Disk usage |
| `du -sh <dir>` | Directory size |
| `free -h` | Memory usage |
| `uptime` | System uptime |
| `hostname` | Show hostname |
| `top` | Show processes |
| `uname -a` | Kernel info |
| `lscpu` | Displays detailed information about the CPU architecture|

---

## 📋 Shell & Environment

| Command | Description |
|--------|-------------|
| `echo $SHELL` | Current shell |
| `alias` | Show aliases |
| `history` | Show command history |
| `export VAR=value` | Set environment variable |
| `printenv` | List environment vars |
| `which <command>` | Show command location |

---

## 💾 Disk Operations

| Command | Description |
|--------|-------------|
| `mount /dev/sdX /mnt` | Mount device |
| `umount /mnt` | Unmount device |
| `fdisk -l` | List partitions |
| `lsblk` | Block devices |
| `mkfs.ext4 /dev/sdX1` | Format partition |

---

## 📝 Text Editors

| Command | Description |
|--------|-------------|
| `nano <file>` | Simple text editor |
| `vim <file>` | Advanced editor |
| `code <file>` | Open in VSCode (if installed) |

---

# Linux Terminal Shortcuts Cheat Sheet

| Shortcut | Description |
|---------|-------------|
| `Ctrl + A` | Move cursor to the **start** of the line |
| `Ctrl + E` | Move cursor to the **end** of the line |
| `Ctrl + U` | Delete from **cursor to start** of the line |
| `Ctrl + K` | Delete from **cursor to end** of the line |
| `Ctrl + W` | Delete the **previous word** |
| `Ctrl + Y` | Paste the last cut text |
| `Ctrl + C` | Terminate the current running process |
| `Ctrl + D` | Logout from terminal / send **EOF** |
| `Ctrl + Z` | Pause the current process (**send to background**) |
| `Ctrl + L` | Clear the terminal screen (same as `clear`) |
| `Ctrl + R` | Search through command history |
| `Ctrl + P` / `Up Arrow` | Show the **previous command** |
| `Ctrl + N` / `Down Arrow` | Show the **next command** |
| `Alt + B` | Move **backward one word** |
| `Alt + F` | Move **forward one word** |
| `Tab` | Auto-complete files and commands |
| `Tab Tab` | List all possible completions |
| `!!` | Run the **last command again** |
| `!abc` | Run the last command starting with `abc` |
| `Ctrl + _` | Undo last action (bash 5+ only) |

---
# Linux Input/Output Redirection Operators

In Linux, redirection operators are used to control where the **input comes from** and where the **output goes to**. These are essential tools in any Linux user’s workflow.

---

## 🔹 Redirection Symbols Explained

| Symbol | Meaning | Example | Description |
|------|---------|---------|-------------|
| `>` | Redirect output to a file (**overwrite**) | `echo "Hello" > file.txt` | Saves the output to a file, replacing its content if it already exists. |
| `>>` | Redirect output to a file (**append**) | `echo "Hello" >> file.txt` | Adds the output to the end of a file without removing the existing content. |
| `<` | Redirect input from a file | `cat < file.txt` | Takes the contents of a file as input for a command. |
| `<<` | Here Document (**multi-line input**) | See example below | Allows you to provide multiple lines of input directly in the command, ending with a specified delimiter. |

---

## 🔹 Detailed Examples

### ➤ `>` Example
```bash
echo "Linux is powerful" > message.txt
```
