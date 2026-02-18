📀 Disk & Storage Management Notes (Linux + AWS)
1️⃣ Understanding Block Devices

In Linux, disks and partitions are treated as block devices.

Examples:

/dev/sda → First disk

/dev/sda1 → First partition on disk

/dev/xvdf → Common AWS EBS disk naming

2️⃣ lsblk – List Block Devices
🔹 Command:
lsblk

🔹 Purpose:

Displays all block devices in a tree format.

🔹 Shows:

Disk name

Size

Type (disk/part)

Mount point

🔹 Example Output:
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda      8:0    0  20G  0 disk
├─sda1   8:1    0  19G  0 part /
└─sda2   8:2    0   1G  0 part [SWAP]

🔹 Useful Options:
lsblk -f        # Shows filesystem type
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT

3️⃣ fdisk -l – View Disk Partition Information
🔹 Command:
fdisk -l

🔹 Purpose:

Lists all disks and their partition details.

🔹 Shows:

Disk size

Sector size

Partition table type (MBR/GPT)

Partition details

🔹 Use Case:

Check new disk after attaching it to a server.

4️⃣ Creating a Volume in AWS and Attaching to Instance

In Amazon Web Services, storage is provided using EBS (Elastic Block Store).

🔹 Steps to Create & Attach Volume:

Go to EC2 Dashboard

Click Elastic Block Store → Volumes

Click Create Volume

Choose:

Size (e.g., 10GB)

Availability Zone (must match EC2 instance)

Click Create

Select volume → Click Attach

Choose EC2 instance

## Disk & Storage Management (Linux + AWS)

### Overview
This note documents common disk and storage management tasks on Linux systems and in AWS (EBS volumes). It covers device identification, partitioning, formatting, mounting, and persistent mounts.

### Block Devices
In Linux, disks and partitions are represented as block devices under `/dev`.

Examples:

- `/dev/sda` — first disk
- `/dev/sda1` — first partition on the first disk
- `/dev/xvdf` — typical AWS EBS device name

### List Block Devices — `lsblk`
Command:

```bash
lsblk
```

Useful options:

```bash
lsblk -f
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT
```

Example output:

```
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda      8:0    0  20G  0 disk
├─sda1   8:1    0  19G  0 part /
└─sda2   8:2    0   1G  0 part [SWAP]
```

### View Partition Tables — `fdisk -l`
Command:

```bash
fdisk -l
```

Purpose: list disks, partition tables (MBR/GPT), sizes, and partition layouts.

### AWS: Create and Attach an EBS Volume
Steps (high level):

1. EC2 Console → Elastic Block Store → Volumes → Create Volume (choose size and AZ).
2. Select the volume → Attach → choose the instance.
3. On the instance, verify the new disk appears with `lsblk` (e.g., `/dev/xvdf`).

### Create a Partition (optional)
To create a partition interactively:

```bash
sudo fdisk /dev/xvdf
# inside fdisk: n (new), p (primary), w (write)
```

Then refresh and verify with `lsblk`.

### Format the Device — `mkfs`
Examples:

```bash
# Format as ext4
sudo mkfs.ext4 /dev/xvdf

# Format as XFS
sudo mkfs.xfs /dev/xvdf
```

Verify filesystem details:

```bash
lsblk -f
```

### Mounting
Create a mount point and mount the device:

```bash
sudo mkdir -p /data
sudo mount /dev/xvdf /data
```

Verify with:

```bash
df -h
```

### Unmounting

```bash
sudo umount /data
# or
sudo umount /dev/xvdf
```

If unmount fails, check open files:

```bash
sudo lsof /data
```

### Make Mount Permanent (`/etc/fstab`)
Prefer using UUIDs to avoid device name changes.

Find UUID:

```bash
sudo blkid /dev/xvdf
# example output: UUID="xxxx-xxxx" TYPE="ext4"
```

Then add to `/etc/fstab`:

```
UUID=xxxx-xxxx   /data   ext4   defaults   0 0
```

Test fstab entries without rebooting:

```bash
sudo mount -a
```

### Quick Command Reference

| Command | Purpose |
|---|---|
| `lsblk` | List block devices |
| `fdisk -l` | View disk partitions |
| `fdisk /dev/xvdf` | Create partition interactively |
| `mkfs.ext4` | Format as EXT4 |
| `mkfs.xfs` | Format as XFS |
| `mount` | Mount filesystem |
| `umount` | Unmount filesystem |
| `df -h` | Check disk usage |
| `blkid` | Show device UUIDs |

---

If you want, I can also:

- add example commands for resizing volumes (AWS + Linux),
- include SELinux/XFS mount options, or
- create a short script to automate attach/format/mount.
