
# What is Volume Mounting?
**Volume mounting** is the process of making a storage volume (partition, disk, or cloud volume) accessible to the operating system by attaching it to a directory in the filesystem.  
Once mounted, you can read, write, and manage data on that volume from the mount point.

In Linux:
- You mount volumes using the `mount` command.
- The mount point is simply a directory (e.g., `/mnt/data`) where the volume’s contents will appear.

## Basic Requirements for Mounting a Volume

On a Local Linux System:
-Formatted Volume – Must have a supported filesystem (e.g., ext4, xfs).
-Mount Point – An empty directory where the volume will be mounted.
-Permissions – Root or sudo privileges to mount/unmount.
-Device Recognition – The OS should detect the device (check with lsblk).

## On Cloud Platforms (e.g., AWS EC2):

-When attaching and mounting EBS Volumes:
-Same Region – The volume must be in the same AWS region as the EC2 instance.
-Same Availability Zone (AZ) – EBS volumes are bound to a single AZ; both instance and volume must be in the same AZ.
-Volume State – The volume must be in the available state before attaching.

**Example:**
```bash
sudo mount /dev/sdb1 /mnt/data
