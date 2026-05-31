Day 13 – Linux Volume Management (LVM) Summary
Task 1: Create Virtual Disk

Purpose: Create a virtual disk for LVM practice.

Commands Used:

sudo -i → Switch to root user
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024 → Create a 1GB virtual disk file
losetup -fP /tmp/disk1.img → Attach file as loop device
losetup -a → Verify loop device mapping
lsblk → View block devices
pvs → Check existing Physical Volumes
vgs → Check existing Volume Groups
Task 2: Create Physical Volume (PV)

Purpose: Initialize disk for LVM.

Command:

pvcreate /dev/loop0

Verification:

pvs
Task 3: Create Volume Group (VG)

Purpose: Create a storage pool from the physical volume.

Command:

vgcreate devops-vg /dev/loop0

Verification:

vgs
Task 4: Create Logical Volume (LV)

Purpose: Create a logical partition from the volume group.

Command:

lvcreate -L 500M -n app-data devops-vg

Verification:

lvs
Task 5: Create Filesystem

Purpose: Format the logical volume for data storage.

Command:

mkfs.ext4 /dev/devops-vg/app-data
Task 6: Mount Logical Volume

Purpose: Make the storage accessible.

Commands:

mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data

Verification:

df -h /mnt/app-data
Task 7: Extend Logical Volume

Purpose: Increase storage without recreating the volume.

Commands:

lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data

Verification:

df -h /mnt/app-data
Important LVM Concepts
Physical Volume (PV)

The actual disk or partition used by LVM.
Example:
/dev/loop0

Volume Group (VG)

A storage pool created from one or more Physical Volumes.
Example:
devops-vg

Logical Volume (LV)

A virtual partition created from a Volume Group.
Example:
app-data

Filesystem

The structure used to store files on a Logical Volume.
Example:
ext4

LVM Flow

Disk/File → Physical Volume (PV) → Volume Group (VG) → Logical Volume (LV) → Filesystem → Mount Point

Example:

disk1.img
↓
/dev/loop0 (PV)
↓
devops-vg (VG)
↓
app-data (LV)
↓
ext4 Filesystem
↓
/mnt/app-data

Key Learning
LVM allows flexible storage management.
Storage can be expanded without recreating partitions.
PV → VG → LV is the core LVM architecture.
lvextend increases LV size.
resize2fs expands the filesystem after extending the LV.
LVM is widely used in Linux production servers and cloud environments.
