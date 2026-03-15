## Q1 What is linux
Linux is a free, open-source operating system based on Unix that was created by
Linus Torvalds in 1991. It manages the communication between software
applications and hardware resources like processors, memory, and devices.
Talk about benefits

## Q2 What is a Linux Kernel? Why is it important?
The Linux kernel is the core component of the Linux operating system that acts as
the main interface between a computer's hardware and its software processes. It
manages system resources and handles communication between hardware
components and applications, ensuring efficient and secure operation

Primary Functions
The kernel performs four critical jobs that make the operating system functional:

- Memory management: Tracks how much memory is used, what data is stored
where, and allocates memory to processes as needed

- Process management: Determines which processes can use the CPU, when,
and for how long, while scheduling and executing processes fairly

- Device drivers: Acts as a mediator between hardware devices and software
processes, providing a standardized way for different hardware types to
interact with the OS

- Network Management :Network management in Linux involves both kernel-
level packet processing and system-level configuration tools that enable
devices to connect, communicate, and maintain network connectivity.

## Q3 What is a shell in Linux, and how is it different from bash?
Sh stands for "Shell" and is also called the Bourne Shell. It's the original Unix shell
created by Stephen Bourne in the 1970s. A shell is a program that acts as an interface
between you and the operating system. It interprets commands you type and tells the
operating system what to do.

Key Characteristics
- POSIX Compliant: Sh follows the POSIX (Portable Operating System Interface) standard, a set of rules that makes shells compatible across different Unix-like operating systems
- Minimal Features: Designed to be simple, lightweight, and basic
- Portable: Works on almost all Unix-like systems (Linux, macOS, BSD, etc.)
- Standardized: Defined by the POSIX standard, not by any single vendor
- Older Syntax: Uses simpler, more traditional command syntax

Bash (Bourne Again Shell) is a specific type of shell, not a separate category.
- Key Characteristics
- Enhanced Version of Sh: Bash takes everything from Sh and adds more powerful features
- Default Shell: The default login shell on most Linux distributions and macOS
- Feature-Rich: Supports arrays, functions, advanced arithmetic, string manipulation, and more
- User-Friendly: Better command-line editing, auto-completion, and command history
- More Flexible: Has advanced scripting capabilities for complex automation tasks
- Not Strictly POSIX: Bash has many extensions that don't follow POSIX standards strictly

## Q4 What are the basic components of a Linux OS?

1️⃣ Kernel (Most Important)
What it is
The kernel is the core of Linux.
What it does
• Manages CPU and processes
• Manages memory
• Controls devices
• Handles file systems
• Manages networking
Simple line:
Kernel = brain of Linux
If kernel stops → system stops.

2️⃣ Shell (User Interface)
What it is
The shell is an interface that allows users to interact with the kernel.
What it does
• Takes user commands
• Interprets them
• Sends them to the kernel
• Displays output
Examples:
• bash
• sh
• zsh
DevOps work happens mostly here.

3️⃣ File System
What it is
The file system organizes data and files on disk.
What it includes
• / (root)
• /etc (config files)
• /var (logs)
• /home (user data)
• /bin, /usr/bin (commands)
Simple line:
Everything in Linux is a file.

4️⃣ System Utilities (Core Tools)
What they are
System utilities are basic programs that help manage the system.
Examples:
• ls, cp, mv
• ps, top
• df, du
• chmod, chown
These tools make Linux usable and manageable.

5️⃣ Applications / User Programs
What they are
These are programs installed by users or admins.
Examples:
• nginx
• docker
• git
• python
• kubectl
They run in user space, not kernel space.

6️⃣ Hardware (Underlying Layer)
What it is
Physical components like:
• CPU
• RAM
• Disk
• Network interface

## Q5. What is the init process in Linux?
The init process is the first process started by the Linux kernel during system boot
and has PID 1.
It is responsible for starting and managing system services and ensuring the system
reaches a usable state.
Modern Linux systems use systemd as the init system, which provides faster startup,
service management, and better reliability.

## Q6. How do you find files in Linux?
In Linux, files can be found using commands like find, locate, which, and whereis.
The find command is the most powerful as it searches files in real time based on
name, type, size, or modification time.
locate provides faster searches using a database, while which and whereis are
mainly used to locate command binaries and related file

## Q7. What is the difference between a soft link and a hard link?
What is a Link in Linux? (quick base)
A link is a reference to a file.
Linux supports two types of links:
• Hard Link
• Soft Link (Symbolic Link)
A soft link is like a shortcut that points to a file path, so if the original file is removed,
the link breaks.
A hard link points directly to the same inode, so even if the original file is deleted,
the data remains accessible.

## Q8. How do you change file permissions in Linux using the chmod command?
Permission means who can do what
Linux file permissions are categorized into three types (read, write, execute) for three
user classes (owner (o), group (g), others (o)).
chmod (change mode) is a Linux command used to change file or directory
permissions.
So we can modify permission using way
Symbolic Mode (Human-friendly). ( + means assign and , - means remove )
Examples:
Add execute permission to owner:
chmod u+x script.sh
Remove write permission from group:
chmod g-w file.txt
Give read permission to others:
chmod o+r file.txt
Give full permission to owner:
chmod u+rwx file.txt
Numeric (Octal) Mode
Permission values:
• r = 4
• w = 2
• x = 1
Numeric examples:
Full permission to owner, read-only to others:
chmod 744 file.txt
Owner full, group read/execute, others no access:
chmod 750 file.txt
Everyone full access:
chmod 777 file.txt (not recommended)

## Q9. What are the different types of permissions available for files in Linux?
Linux provides three main types of file permissions: read, write, and execute.
These permissions are applied to three categories: owner, group, and others.
Read allows viewing content, write allows modification, and execute allows
running a file or accessing a directory.
Together, these permissions help maintain security and controlled access in a multi-
user Linux environment.

## Q10. How do you create and manage symbolic links?
Basic command
ln -s <target> <link_name>

## Q11. How do you check your current path/directory?
Using pwd cmd

## Q12. How do you combine two commands, and what is the use of a pipe (|) in Linux?
What is a Pipe (|)? (easy words)
A pipe (|) takes the output of one command and sends it as the input to another
command.
How Pipe Works (simple flow)
command1 | command2

## Q13. How can you check for free disk space?
Command Purpose
df Free/used disk
space
du Directory size
lsblk Disk structure
Free disk space in Linux can be checked using the df command, especially df -h,
which shows disk usage in a human-readable format.
To analyze space used by specific directories, the du command can be used, while
lsblk helps understand disk and partition structure.

## Q15. What are the different ways to view the content of a file without using the cat command?
Command Use Case
less Large files,
scrolling
more Simple paging
head Beginning of file
tail End of file, logs
sed Specific lines
awk Structured output

## Q16. How do you check the current IP address of your Linux server?
The current IP address of a Linux server can be checked using commands like ip
addr or hostname -I, which display assigned network interfaces and IP addresses.
For older systems, ifconfig can be used, while public IP addresses can be checked
using tools like curl ifconfig.me.
These methods are commonly used in system administration and DevOps
environments.


## Q17. What is SSH, and how is it used to access a Linux server remotely?
SSH (Secure Shell) is a secure protocol used to remotely access and manage Linux
servers over a network.
It encrypts all communication between the client and the server, ensuring secure
authentication and data transfer.
SSH is commonly used by administrators and DevOps engineers to log in to servers,
execute commands, and manage systems remotely.

## Q18. What is a package manager in Linux, and why is it useful?
A package manager in Linux is a tool used to install, update, remove, and manage
software packages.
It automatically handles dependencies, ensures secure and consistent installations,
and simplifies system maintenance.
Package managers such as APT, YUM, and DNF are widely used in Linux and
DevOps environments for efficient software management.

## Q19. How do you terminate an ongoing process in Linux?
An ongoing process in Linux can be terminated by sending signals using commands
like kill, pkill, or killall.
The kill command sends a signal to a process using its PID, where SIGTERM is
used for graceful termination and SIGKILL is used for forceful termination.
Processes can also be stopped interactively using Ctrl + C.

## Q20. How do you check system architecture and CPU/memory stats?
System architecture in Linux can be checked using commands like uname -m, arch,
or lscpu, which provide details about CPU architecture and cores.
CPU usage can be monitored using top or htop, while memory statistics can be
checked using free -h, vmstat, or /proc/meminfo.
These tools are commonly used by administrators and DevOps engineers to monitor
and analyze system performance.


## Q21 What is the I/O Stack?
“The Linux I/O stack describes how data flows from an application to the hardware.
It starts from the application layer, goes through system calls, VFS, filesystem, block
layer, device drivers, and finally reaches the disk

## Q22 what is the different between LVM and PV?
PV stands for Physical Volume, which is a physical disk or partition used by LVM.
LVM stands for Logical Volume Manager, which manages storage by combining
one or more PVs into Volume Groups and creating Logical Volumes. LVM provides
flexibility like resizing, snapshotting, and better disk management, which is not
possible with PV alone.”

## Q23 If a Disk Is Failing, How Do You Troubleshoot It?
If a disk is failing, I first identify symptoms by checking disk usage and mount status
using df -h and lsblk.
I then analyze system logs using dmesg or journalctl for I/O errors and check disk
health using SMART tools like smartctl.
If the disk shows signs of failure, I immediately take backups or snapshots,
minimize disk writes, and replace the disk or attach a new volume in cloud
environments.
Finally, I validate the system and implement monitoring to prevent future failures.


## Q24 What is LILO?
LILO (Linux Loader) is an older boot loader used in Linux systems to load the Linux
kernel into memory during system startup.
It transfers control from the BIOS to the Linux operating system and allows basic
OS selection.
LILO has largely been replaced by GRUB, which offers better flexibility, recovery
features, and modern file system support.


## Q25 tell me about different type of file systems
- 1️⃣ EXT File Systems (Most Common)
🔹 EXT4 (Most used ✅)
• Default Linux file system
• Fast, stable, reliable
• Supports large files & disks
• Journaling supported
Used in:
Servers, cloud VMs, laptops
Other EXT versions:
• EXT2 → no journaling (older)
• EXT3 → journaling added
Interview tip:
EXT4 is the standard Linux file system.

- 2️⃣ XFS (High-performance)
• Designed for large files
• Very fast I/O
• Excellent for databases
• Journaling supported
Used in:
• RHEL, CentOS
• Large production servers
Downside:
• Shrinking is difficult

- 3️⃣ Btrfs (Modern & Advanced)
• Snapshot support
• Built-in RAID
• Compression
• Copy-on-write
Used in:
• Modern Linux setups
• Advanced storage use cases
Still evolving.

- 4️⃣ FAT / FAT32
• Simple file system
• Compatible with Windows, Linux, macOS
• No permissions
• File size limit
Used in:
• USB drives
• Pen drives

- 5️⃣ NTFS
• Windows file system
• Supports large files
• Linux can read/write NTFS
Used when:
• Sharing disks with Windows

- 6️⃣ Swap File System
• Used as virtual memory
• Helps when RAM is full
Used for:
• Performance support
• System stability
Command example:
swapon -s

- 7️⃣ Network File Systems
🔹 NFS
• Linux ↔ Linux sharing
🔹 CIFS / SMB
• Linux ↔ Windows sharing
Used in:
• Enterprise environments
• Shared storage

- 8️⃣ Virtual / Pseudo File Systems
These don’t store real data.
File
System Purpose
/proc Process & kernel info
/sys Hardware & kernel info
tmpfs Temporary memory- based FS

## Q26 what is partition in linux
A partition in Linux is a logical division of a physical disk that allows the disk to be
organized into separate storage areas.
Each partition can have its own file system and be mounted independently for
different purposes such as the root directory, home directory, or swap space.
Partitioning improves data organization, security, and system management.


## Q27 What is the swap space ?
Swap space in Linux is a portion of disk used as virtual memory when physical RAM is exhausted.
It helps prevent system crashes by moving inactive memory pages from RAM to disk.
Swap improves system stability but is slower than RAM, so it should be used
carefully in performance-critical environments.


## Q28 What is the sudoers file in Linux?
The sudoers file defines who can run which commands as root (or another user)
using sudo.


## Q28 What are daemons in Linux?
Daemons in Linux are background processes that run continuously to provide system
or application services.
They usually start at system boot and do not require user interaction, handling tasks
such as networking, logging, scheduling, and web services.


## Q29 What is grep command, and how is it useful on Linux?
grep (Global Regular Expression Print) is a command used to search for specific
text or patterns inside files or command output.

## Q30 How do you secure a Linux server?
Create a strong password
Update the server and apply security patches.
Use secured protocols like SSH and configure it to use key-based authentication for
higher security.
Use the intrusion detection system (IDS) to monitor network traffic and prevent
malicious activities.
Configure the firewall to limit the inbound and outbound traffic on the server.
Disable all unused network services.
Create regular backups.
Review logs and perform regular security audits.
Encrypt network traffic and enable monitoring.

## Q31 What is the difference between absolute and relative paths in Linux?
Absolute path = It specifies the exact location of a file or directory from the root
directory ("/"). We will notice that they always start with a forward slash ("/").
For Example: `/home/user/jayesh/geeksforgeeks.txt`
Relative paths = It specifies the location relative to the current working directory. In
this we do not start with a forward slash ("/").
For Example: `documents/file.txt`


## Q32 How do you compress and decompress files in Linux?
In Linux, files can be compressed and decompressed using tools such as tar, gzip,
zip, bzip2, and xz.
The tar command combined with compression options like gzip is commonly used
to archive and compress directories, while tools like gunzip and unzip are used for
decompression.

## Q33 What is the sed command used for in Linux?
The sed command in Linux is a stream editor used to perform text transformations
such as search, replace, insert, and delete operations on files or command output.


## Q34 What is the awk command used for in Linux?
The awk command in Linux is used to process and analyze structured text data by
working with fields and records.
It is commonly used to extract specific columns, apply conditions, and format
output from files or command results.
awk is widely used in system administration and DevOps for log analysis and
automation.


## Q35 What are inodes and what data do they store?
An inode in Linux is a data structure that stores metadata about a file, such as
permissions, ownership, size, timestamps, and pointers to the data blocks.
It does not store the file name or the actual file content.
Directories map file names to inode numbers, which allows features like hard links
and efficient file system management.

## Q36 As a DevOps Engineer, how would you manage resource allocation for different users and processes in a Linux system?
You can use the ulimit command to set user-level limits on system resources, such
as maximum file size, CPU time, and memory usage.
But, for more granular control, you can use Control Groups (cgroups) to limit,
account for, and isolate resource usage for groups of processes.

## Q37 How do you troubleshoot network connectivity issues in a Linux system?
One of the most basic commands is the ping command, which can verify if the
network and the host are reachable. The traceroute command is also useful as it
shows the path a packet takes to reach the host. Moreover, netstat is another powerful
command used to display a variety of network-related information.


## Q38 What is shell scripting, and how have you used it in your previous roles?
"In my previous roles, I've used shell scripting to automate various tasks. For
example, I wrote a script to back up certain directories on our server every night
using tar and scp commands. This automation saved time and reduced the risk of
errors compared to performing the task manually.

## Q39 Write a script for the backups
#!/bin/bash
# folder to backup
SOURCE="/home/user/data"
# backup location
DEST="/home/user/backup"
# date
DATE=$(date +%F)
# create backup folder if not exists
mkdir -p $DEST
# create backup
tar -czf $DEST/backup-$DATE.tar.gz $SOURCE
echo "Backup completed"

## Q40 what is cron tab
Crontab is a Linux scheduler used to automate tasks by running commands or scripts
at specified times or intervals.
It is commonly used for backups, maintenance jobs, and routine system tasks without
manual intervention.

## Q41 How do you check and manage system logs in Linux?
System logs are stored in /var/log. Tools like journalctl (for systemd systems) and
logrotate help view and manage logs. Logs include boot messages, authentication
attempts, and service errors. Monitoring logs is crucial for debugging and
maintaining system health.


## Q42 sudo vs su
su is used to switch to another user, usually root, and requires the root password,
giving full administrative access.
sudo allows a user to execute specific commands with elevated privileges using
their own password and is controlled by the sudoers file.


## Q43 User & group management
Linux user and group management is used to control who can access the system and
files.
Users are individual accounts, and groups are used to manage permissions for
multiple users together.
This helps keep the system secure and easy to manage, especially in production
environments.


## Q44 What is the zombie process in linux
A zombie process in Linux is a process that has completed execution but still
has an entry in the process table because the parent process hasn’t collected its
exit status using wait() or waitpid().
The process is no longer running and doesn’t consume CPU or memory, but it still
holds a PID.
If many zombie processes accumulate, they can exhaust the PID table, which may
prevent new processes from being created.

## Q45 fstab in linux
fstab is a configuration file located at /etc/fstab that defines static information about
filesystems, including what to mount, where to mount, and how to mount them
automatically during system startup.

## Q46 What is an Orphan Process in Linux?
An orphan process is a process whose parent process has finished or crashed,
but the child process is still running.
🔗 How it actually happens (classic UNIX behavior)
1. A parent process creates a child using fork()
2. Parent process exits early (intentionally or by crash)
3. Child process is still running
4. Boom → Orphan process created

## Q47 What is Log Rotation?
Log rotation is the automated process of managing log files by rotating, compressing,
and deleting old logs to prevent disk space issues and maintain system stability.


## Read commands https://github.com/SaimShaikh/Linux_For_DevOps/tree/main
