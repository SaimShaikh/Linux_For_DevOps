# Linux for DevOps – Complete Notes & Interview Prep

---

## My Introduction

"Good afternoon/ morning. My name is Saime Shaikh, and I’m from Indapur, Maharashtra.  
I completed my B.Tech in Cloud Technology and Information Security at Ajeenkya DY Patil University in Pune, and I also hold a diploma in Computer Engineering from Vidya Pratishthan Polytechnic College.

For the past nine months, I’ve been working as a DevOps intern at Hisan Labs Private Limited. In this role, I’ve had the opportunity to dive into a range of cloud and DevOps tools, including Docker, Kubernetes, Grafana, Prometheus, AWS, Linux, Git, GitHub, and ArgoCD.

One of my main responsibilities has been working on projects like building secure CI/CD pipelines and deploying applications on AWS EKS. I’ve also had the chance to enhance client data workflows using cloud-native platforms, which really sharpened my problem-solving skills and deepened my understanding of these tools.

I’m always eager to learn new technologies and continuously improve as a DevOps engineer. I’m looking forward to discussing how my experience can be a great fit for this full-time role. Thanks for the opportunity."

---

## How to Explain Jenkins Pipeline

"In our Jenkins CI/CD pipeline, we've implemented a comprehensive multi-stage workflow to ensure both quality and security at every step. We start by automatically cloning the latest code from our Git repository. Once the code is pulled in, we move into the build stage where we create a Docker image from that source code.

After the image is built, we push it securely to Docker Hub, ensuring we follow best practices for image storage. Then we run a series of rigorous checks: we use SonarQube to perform static code analysis and maintain code quality. We run Trivy and OWASP ZAP scans to identify any vulnerabilities or security issues in the code and the container. We also incorporate Docker Scout to ensure our images comply with our standards and policies.

Once the image passes all these quality gates, we proceed to deploy it to our Kubernetes cluster. We've also added an email notification system so that the DevOps team is instantly alerted to the status of the deployment, whether it succeeds or fails. This entire workflow not only automates our delivery but also ensures that every release is thoroughly tested and secure before it goes live."

---

## Day 1 Linux

### Q1 What is Linux
Linux is a free, open-source operating system based on Unix that was created by Linus Torvalds in 1991. It manages the communication between software applications and hardware resources like processors, memory, and devices.

### Q2 What is a Linux Kernel? Why is it important?
The Linux kernel is the core component of the Linux operating system that acts as the main interface between a computer's hardware and its software processes.

Primary Functions:
- Memory management
- Process management
- Device drivers
- Network management

### Q3 What is a shell in Linux, and how is it different from bash?
Shell is an interface between user and OS.  
Bash (Bourne Again Shell) is an enhanced version of sh with advanced features.

### Q4 Basic Components of Linux OS
- Kernel
- Shell
- File System
- System Utilities
- Applications
- Hardware

### Q5 What is the init process?
The init process is the first process started by the kernel (PID 1). Modern systems use systemd.

### Q6 Finding files in Linux
Commands: find, locate, which, whereis

### Q7 Soft link vs Hard link
- Soft link breaks if original is deleted
- Hard link points to inode

### Q8 chmod command
Symbolic and Numeric modes explained with examples.

### Q9 File permissions
Read, Write, Execute for Owner, Group, Others.

### Q10 Symbolic links
```bash
ln -s <target> <link_name>
```

### Q11 Current directory
```bash
pwd
```

### Q12 Pipe
```bash
command1 | command2
```

### Q13 Disk space
df, du, lsblk

### Q15 View file content without cat
less, more, head, tail, sed, awk

### Q16 Check IP address
ip addr, hostname -I

### Q17 SSH
Secure remote access protocol.

### Q18 Package manager
APT, YUM, DNF

### Q19 Kill process
kill, pkill, killall, Ctrl+C

### Q20 System stats
uname, lscpu, top, free

### Q21 I/O Stack
Application → Syscall → VFS → FS → Block → Driver → Disk

### Q22 LVM vs PV
PV = Physical Volume  
LVM = Logical Volume Manager

### Q23 Disk failure troubleshooting
df, lsblk, dmesg, smartctl, backup & replace

### Q24 LILO
Old bootloader replaced by GRUB

### Q25 File systems
EXT4, XFS, Btrfs, FAT, NTFS, Swap, NFS, CIFS, proc, sys, tmpfs

### Q26 Partition
Logical division of disk

### Q27 Swap space
Disk used as virtual memory

### Q28 sudoers file
Defines sudo permissions

### Q28 Daemons
Background services

### Q29 grep
Search text/patterns

### Q30 Secure Linux server
Passwords, updates, SSH keys, firewall, IDS, backups

### Q31 Absolute vs Relative path

### Q32 Compress & Decompress
tar, gzip, zip, bzip2

### Q33 sed
Stream editor

### Q34 awk
Text processing

---

## Day 2 Linux

### Q35 Inodes
Stores metadata, not filename or data

### Q36 Resource allocation
ulimit, cgroups

### Q37 Network troubleshooting
ping, traceroute, netstat

### Q38 Shell scripting usage
Automation example

### Q39 Backup Script
```bash
#!/bin/bash
SOURCE="/home/user/data"
DEST="/home/user/backup"
DATE=$(date +%F)
mkdir -p $DEST
tar -czf $DEST/backup-$DATE.tar.gz $SOURCE
echo "Backup completed"
```

### Q40 Crontab
Scheduler for automation

### Q41 System logs
/var/log, journalctl, logrotate

### Q42 sudo vs su

### Q43 User & group management

### Q44 Zombie process

### Q45 fstab
Filesystem mount config

### Q46 Orphan process

### Q47 Log rotation

---

## Reference
https://github.com/SaimShaikh/Linux_For_DevOps/tree/main
