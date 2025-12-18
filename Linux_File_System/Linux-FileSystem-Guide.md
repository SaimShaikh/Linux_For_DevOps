# Linux File Systems: Complete Guide

> Simple explanations of different Linux file systems. Easy to understand and remember.

---

## What is a File System?

A **file system** is a method of organizing and storing files on a disk.

Think of it like a filing cabinet:
- Without a system: files are scattered randomly
- With a system: files are organized in folders with labels

**File system manages:**
- How files are stored on disk
- How to find files quickly
- File permissions and ownership
- Disk space allocation
- File recovery if deleted

---

## Main Linux File Systems

| File System | Year | Max File Size | Max Volume | Use Case |
|------------|------|---------------|-----------|----------|
| **ext4** | 2008 | 16 TB | 1 EB | Most common, default |
| **ext3** | 2001 | 2 TB | 16 TB | Older systems |
| **ext2** | 1993 | 2 GB | 2 TB | Very old |
| **XFS** | 1993 | 8 EB | 8 EB | High-performance servers |
| **Btrfs** | 2007 | 16 EB | 16 EB | Modern, with snapshots |
| **ZFS** | 2005 | 16 EB | Unlimited | Enterprise storage |
| **NTFS** | 1995 | 16 EB | 16 EB | Windows (Linux support) |
| **FAT32** | 1996 | 4 GB | 2 TB | USB drives, old systems |
| **exFAT** | 2006 | 16 EB | 512 TB | Modern USB drives |

---

## 1. ext4 (Fourth Extended File System)

**Most common Linux file system.**

### Characteristics

- Released: 2008
- Default on: Ubuntu, Debian, CentOS
- Max file size: 16 TB
- Max volume: 1 EB (exabyte)
- Journaling: Yes (prevents corruption)
- Backward compatible: Yes (with ext3)

### How It Works

```
Inode: Pointer to file location and metadata
|
├── File 1 (Size, permissions, owner)
├── File 2 (Size, permissions, owner)
└── Directory structure
```

### Advantages

✅ Stable and reliable
✅ Good performance
✅ Journal recovery (corruption-resistant)
✅ Supports large files (16 TB)
✅ Widely supported
✅ Low overhead

### Disadvantages

❌ Older technology
❌ Not optimized for SSDs
❌ No snapshots
❌ No built-in compression

### When to Use

- Desktop Linux (Ubuntu, Fedora)
- Server (Linux VM on AWS/Azure)
- General-purpose storage

### Check if Your System Uses ext4

```bash
df -T
# Output: /dev/sda1  ext4  20G  ...

# Or check specific mount point
df -T /

# Or use lsblk
lsblk -f
```

---

## 2. ext3 (Third Extended File System)

**Predecessor to ext4. Still used on older systems.**

### Characteristics

- Released: 2001
- Max file size: 2 TB
- Max volume: 16 TB
- Journaling: Yes (first to have it)
- Backward compatible: ext2

### Advantages

✅ First to introduce journaling (faster recovery)
✅ Stable
✅ Good for older systems

### Disadvantages

❌ Outdated (ext4 is better)
❌ Smaller file size limit (2 TB)
❌ Slower than ext4
❌ Limited features

### When to Use

- Old CentOS/RHEL servers
- Legacy systems

**Avoid for new systems** – use ext4 instead.

---

## 3. ext2 (Second Extended File System)

**Very old. Rarely used today.**

### Characteristics

- Released: 1993
- Max file size: 2 GB
- Max volume: 2 TB
- Journaling: No (why ext3 was created)
- Speed: Fast on hardware with limitations

### Disadvantages

❌ No journaling (can corrupt if power fails)
❌ Very small file size limit (2 GB)
❌ Outdated

### When to Use

- USB drives (sometimes for compatibility)
- Floppy disks (historically)
- NOT for modern systems

---

## 4. XFS (eXtended File System)

**High-performance file system for large files and servers.**

### Characteristics

- Released: 1993 (SGI)
- Max file size: 8 EB
- Max volume: 8 EB
- Journaling: Yes
- Performance: Excellent for large files
- Used by: AWS, enterprise Linux

### How It's Different

- Optimized for parallel I/O
- Dynamic inode allocation
- Extent-based allocation (faster)
- No defragmentation needed

### Advantages

✅ Excellent performance on large files
✅ Large volume support (8 EB)
✅ Parallel processing
✅ No fragmentation issues
✅ Used by AWS instances
✅ Great for video/database servers

### Disadvantages

❌ Cannot shrink volumes (only grow)
❌ Less portable than ext4
❌ Newer (not default everywhere)
❌ No online shrinking

### When to Use

- AWS instances (EC2)
- High-performance servers
- Large file storage (video, database)
- Enterprise environments

### Check and Format

```bash
# Check if XFS is available
lsblk -f

# Format a partition as XFS
sudo mkfs.xfs /dev/sda1

# Mount XFS
sudo mount -t xfs /dev/sda1 /mnt/data
```

### Real Example: AWS EC2

```bash
# On AWS EC2 instance
df -T
# Output: /dev/nvme0n1p1  xfs  50G  ...
```

---

## 5. Btrfs (B-Tree File System)

**Modern file system with snapshots and compression.**

### Characteristics

- Released: 2007
- Max file size: 16 EB
- Max volume: 16 EB
- Journaling: Copy-on-Write (COW)
- Snapshots: Yes
- Compression: Built-in

### Advanced Features

1. **Snapshots**
   ```bash
   # Create snapshot of /home
   sudo btrfs subvolume snapshot /home /home-backup-2025-12-18
   
   # Restore from snapshot
   sudo btrfs subvolume delete /home
   sudo btrfs subvolume snapshot /home-backup-2025-12-18 /home
   ```

2. **Compression**
   ```bash
   # Mount with compression
   sudo mount -o compress=zstd /dev/sda1 /mnt
   ```

3. **RAID support**
   ```bash
   # Create RAID1 (mirror)
   sudo mkfs.btrfs -d raid1 /dev/sda1 /dev/sda2
   ```

### Advantages

✅ Snapshots (great for backups)
✅ Compression (saves space)
✅ Built-in RAID
✅ Copy-on-Write (safe)
✅ Subvolumes
✅ Modern and flexible

### Disadvantages

❌ Newer (less tested in production)
❌ Complexity
❌ Can be slower than ext4/XFS
❌ Not default on many distros

### When to Use

- OpenSUSE (default file system)
- Fedora workstations
- Backup systems with snapshots
- Home servers

### Check Btrfs Info

```bash
# Check Btrfs filesystems
sudo btrfs filesystem show

# Get usage statistics
sudo btrfs filesystem usage /mnt
```

---

## 6. ZFS (Zettabyte File System)

**Enterprise-grade file system with advanced features.**

### Characteristics

- Released: 2005 (Sun Microsystems)
- Max file size: 16 EB
- Max volume: Unlimited
- Journaling: Copy-on-Write (COW)
- Snapshots: Yes, extremely fast
- Compression: Excellent
- Data integrity: Built-in checksums

### Advanced Features

1. **RAID-Z** (better than traditional RAID)
   ```bash
   # Create RAID-Z (like RAID5)
   sudo zpool create mypool raidz /dev/sda /dev/sdb /dev/sdc
   ```

2. **Snapshots and Clones**
   ```bash
   # Create snapshot
   sudo zfs snapshot tank@backup-2025-12-18
   
   # Clone snapshot
   sudo zfs clone tank@backup-2025-12-18 tank/clone
   ```

3. **Compression**
   ```bash
   # Enable compression
   sudo zfs set compression=lz4 tank
   ```

### Advantages

✅ Enterprise-grade reliability
✅ Advanced RAID (RAID-Z)
✅ Snapshots are instant and lightweight
✅ Compression excellent
✅ Data checksums (detect corruption)
✅ Very scalable
✅ Copy-on-Write

### Disadvantages

❌ Complex
❌ Higher memory usage
❌ Not included in standard Linux (BSD/FreeNAS has it)
❌ License issues (CDDL)
❌ Slower than ext4 for small files

### When to Use

- NAS systems (FreeNAS, TrueNAS)
- Enterprise storage
- Backup systems
- High-reliability requirements

### Install on Linux

```bash
# Ubuntu/Debian
sudo apt-get install zfsutils-linux

# Create ZFS pool
sudo zpool create tank /dev/sda1
```

---

## 7. NTFS (New Technology File System)

**Windows file system, but Linux can read/write it.**

### Characteristics

- Released: 1995
- Max file size: 16 EB
- Max volume: 16 EB
- Journaling: Yes
- Native to: Windows
- Linux support: Yes (via ntfs-3g)

### Advantages

✅ Wide compatibility (Windows, Mac, Linux)
✅ Good for external drives
✅ Large file support

### Disadvantages

❌ Not optimized for Linux
❌ Requires extra package (ntfs-3g)
❌ Slower than native Linux file systems
❌ Designed for Windows

### When to Use

- External USB drives (Windows/Linux sharing)
- Dual-boot systems
- Transferring files between Windows and Linux

### Mount NTFS on Linux

```bash
# Install NTFS support
sudo apt-get install ntfs-3g

# Mount NTFS partition
sudo mount -t ntfs-3g /dev/sda1 /mnt/windows

# Or auto-mount (fstab)
sudo blkid  # Find UUID
# Add to /etc/fstab:
# UUID=xxxxx /mnt/windows ntfs-3g defaults 0 0
```

---

## 8. FAT32 (File Allocation Table)

**Very old file system, used on USB drives and floppies.**

### Characteristics

- Released: 1996
- Max file size: 4 GB
- Max volume: 2 TB
- Journaling: No
- Very simple structure

### Advantages

✅ Universal compatibility (Windows, Mac, Linux, phones)
✅ Simple

### Disadvantages

❌ Very old (1996)
❌ 4 GB file size limit
❌ No journaling (can corrupt)
❌ Inefficient space usage
❌ No permissions/security

### When to Use

- Old USB drives
- Devices requiring maximum compatibility
- **NOT for modern systems**

### Mount FAT32

```bash
# Usually auto-mounts
sudo mount -t vfat /dev/sda1 /mnt/usb

# Format as FAT32
sudo mkfs.vfat -F 32 /dev/sda1
```

---

## 9. exFAT (Extended FAT)

**Modern replacement for FAT32. Better for USB drives.**

### Characteristics

- Released: 2006
- Max file size: 16 EB
- Max volume: 512 TB
- Journaling: No
- Better than FAT32

### Advantages

✅ No 4 GB file size limit
✅ Better compatibility than NTFS
✅ Good for USB drives
✅ Supported on Windows, Mac, Linux

### Disadvantages

❌ No journaling
❌ No permissions
❌ Not ideal for OS installation

### When to Use

- Modern USB drives
- Portable external hard drives
- Cross-platform sharing (Windows/Mac/Linux)

### Mount exFAT on Linux

```bash
# Install exFAT support
sudo apt-get install exfat-utils exfat-fuse

# Mount exFAT
sudo mount -t exfat /dev/sda1 /mnt/usb
```

---

## File System Comparison Table

| Feature | ext4 | XFS | Btrfs | ZFS | NTFS | exFAT |
|---------|------|-----|-------|-----|------|-------|
| **Use Case** | General | High-perf | Modern | Enterprise | Windows | USB drive |
| **Max File** | 16 TB | 8 EB | 16 EB | 16 EB | 16 EB | 16 EB |
| **Journaling** | Yes | Yes | COW | COW | Yes | No |
| **Snapshots** | No | No | Yes | Yes | No | No |
| **Compression** | No | No | Yes | Yes | No | No |
| **RAID** | No | No | Yes | Yes (RAID-Z) | No | No |
| **Default On** | Ubuntu | AWS | OpenSUSE | NAS | Windows | USB |
| **Complexity** | Low | Medium | High | High | Medium | Low |
| **Performance** | Good | Excellent | Good | Excellent | Good | Poor |
| **Reliability** | Good | Good | Excellent | Excellent | Good | Fair |

---

## How to Check Current File System

```bash
# Method 1: df command
df -T
# Output:
# Filesystem     Type     Size  Used Avail Use% Mounted on
# /dev/sda1      ext4      20G   5G   15G  25%  /
# /dev/sdb1      xfs       50G   10G  40G  20%  /home

# Method 2: lsblk command (shows block devices)
lsblk -f
# Output:
# NAME   FSTYPE SIZE TYPE
# sda1   ext4   20G  part  /
# sdb1   xfs    50G  part  /home

# Method 3: blkid (device UUIDs and file systems)
sudo blkid
# Output:
# /dev/sda1: UUID="..." TYPE="ext4"
# /dev/sdb1: UUID="..." TYPE="xfs"

# Method 4: mount command
mount | grep -E "^/dev"
```

---

## How to Format a Disk with Different File Systems

### Format as ext4

```bash
# Warning: This deletes all data!
sudo mkfs.ext4 /dev/sda1

# Label it
sudo mkfs.ext4 -L MyDisk /dev/sda1
```

### Format as XFS

```bash
sudo mkfs.xfs /dev/sda1
```

### Format as Btrfs

```bash
sudo mkfs.btrfs /dev/sda1
```

### Format as FAT32

```bash
sudo mkfs.vfat -F 32 /dev/sda1
```

### Format as exFAT

```bash
sudo mkfs.exfat /dev/sda1
```

---

## How to Mount File Systems

### Temporary Mount (until reboot)

```bash
# Create mount point
sudo mkdir -p /mnt/data

# Mount partition
sudo mount -t ext4 /dev/sda1 /mnt/data

# Verify
df -h /mnt/data

# Unmount
sudo umount /mnt/data
```

### Permanent Mount (survives reboot)

Edit `/etc/fstab`:

```bash
sudo nano /etc/fstab

# Add line:
# /dev/sda1    /mnt/data    ext4    defaults    0 2
# OR use UUID (more reliable):
# UUID=12345678-1234-1234-1234-123456789012    /mnt/data    ext4    defaults    0 2

# Apply changes
sudo mount -a
```

### Mount by UUID (recommended)

```bash
# Find UUID
sudo blkid

# Use UUID in /etc/fstab
UUID=12345678-1234-1234-1234-123456789012 /mnt/data ext4 defaults 0 2
```

---

## File System Selection Decision Tree

```
What do you need?

1. General-purpose Linux?
   → ext4 (default, stable)

2. High-performance server?
   → XFS (AWS, enterprise)

3. Modern laptop/workstation?
   → Btrfs or ext4 (snapshots nice to have)

4. Enterprise NAS/storage?
   → ZFS (maximum reliability)

5. Sharing files between Windows/Mac/Linux?
   → exFAT (USB drive)

6. Legacy system?
   → ext3 (outdated, avoid)

7. Maximum compatibility?
   → NTFS (external drive)
```

---

## File System Performance Comparison

| Operation | ext4 | XFS | Btrfs | ZFS |
|-----------|------|-----|-------|-----|
| **Small files read** | Fast | Fast | Medium | Slow |
| **Large files read** | Good | Excellent | Good | Good |
| **Small files write** | Fast | Fast | Medium | Medium |
| **Large files write** | Good | Excellent | Good | Excellent |
| **Snapshots** | Slow/manual | No | Fast | Very fast |
| **Compression** | No | No | Yes | Yes |
| **RAID rebuild** | Hours | Hours | Hours | Minutes (RAID-Z) |
| **Memory usage** | Low | Medium | Medium | High |

---

## Summary and Recommendations

**For most users:**
- **Desktop**: ext4 (or Btrfs if you want snapshots)
- **Server**: ext4 or XFS
- **AWS/Cloud**: XFS (already configured)
- **NAS/Storage**: ZFS
- **USB drive**: exFAT
- **Cross-platform**: NTFS or exFAT

**Avoid:**
- ext2 (too old)
- ext3 (outdated, ext4 is better)
- FAT32 (4 GB file limit)

**The safe choice:** **ext4** (works everywhere, good performance, stable)

**The modern choice:** **XFS** or **Btrfs** (if your distro supports it)

**The enterprise choice:** **ZFS** (maximum features, reliability)

---

## Quick Reference Commands

```bash
# Check file system type
df -T

# List all file systems
lsblk -f

# Get block device info
sudo blkid

# Format partition
sudo mkfs.ext4 /dev/sda1

# Mount partition
sudo mount -t ext4 /dev/sda1 /mnt

# Unmount
sudo umount /mnt

# Check mounted file systems
mount | grep -E "^/dev"

# Disk usage
sudo du -sh /mnt

# File system repair (ext4)
sudo fsck.ext4 /dev/sda1

# View /etc/fstab
cat /etc/fstab
```

Good luck learning Linux file systems!
