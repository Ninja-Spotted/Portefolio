---
title: "Filesystems"
parent: Computer Architecture
permalink: "/computer_architecture/filesystems"
layout: default
---

### Filesystems

In a storage device, information is localized by its address. Filesystems are the solution that allows the user to organize it into files, identifiable by name, and grouped by folders however, it need a file allocation system (FAT,NTFS,EXT,etc.).

#### Relevant History

Physical disk media history has much effect on everyday since many concepts storage still use vocabulary related to disks.
![](https://images.wondershare.com/recoverit/article/2019/12/sector-track-image.jpg)  
For example:
- Sector: containing 512 bytes.
- Cluster: aka allocation unit, it consists of one or more sectors and represents the minimum amount of space that an operating system allocates for saving a file.

It is possible to check the information about a disk using `hdparm -i /dev/your_disk`. Use `lsblk` to get a list of partitions and disks the system.

#### GPT (GUID Partition Table)
![source](https://learn.microsoft.com/en-us/troubleshoot/windows-server/backup-and-storage/guid-partitioning-table-disk-faq)  
![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/07/GUID_Partition_Table_Scheme.svg/1200px-GUID_Partition_Table_Scheme.svg.png)  
A new way to partition disks, since it can address more sectors, meaning more disk space than MBR, and it has 2 copies of the partition table.  
* LBA0: The first LBA (Logical Block Address) is a protective/dummy Master Boot Record for OS's that cannot read GPT.
* LBA1: Primary Header, defines max number of partitions, disk UUID, etc.
* LBA2-33: Partition Entries with information about them.
* LBA34-...: Partition Data.
* Rest of it is an copy of the GPT (secondary).  

#### Filesystem tools

There are a few important tools:
* Creating Filesystems:

`mkfs -t vfat /dev/sda1`  
`mkfs.ext2 /dev/hda1`  
`mke2fs /dev/sda2`  

* Mounting/Unmounting Filesystems:

Mounting: `mount /dev/hda2 /new/subdir`
Unmounting: `umount /dev/hda2` or `umount /new/subdir`
Automatic mounting (by adding an entry in): `/etc/fstab`

#### Types of Filesystems

* Windows
     * vFAT (Traditional Windows Filesystem) 
     * FAT16 (Compatible with all but maximum of 4 Gb)
     * FAT32 
     * NTFS

* Linux
     * Ext2 (Traditional Linux Filesystem)
     * Ext4
     * Others (reiserFS, JFS, XFS, btrfs)
     * [Squashfs](https://docs.kernel.org/filesystems/squashfs.html#squashfs-4-0-filesystem) (Read-only, compressed, used in most live USB distributions)  
     Fine for kernel and binaries, with great compression rate and access performance
     
 * __*DO NOT USE*__ RAM Disks (Filesystem in RAM, inverse concept of swap which is RAM on disk)  
RAM disks have fixed sizes and are treated like regular disk partitions. This means that we can access it like a physical disc, while being much faster.  
However, all RamDisk data is lost when the system is powered off and/or rebooted.

* [tmpfs](https://docs.kernel.org/filesystems/tmpfs.html#tmpfs)  
Useful to store temporary data in RAM, lives in the Linux file cache and doesn't waste RAM (no duplication). Examples on how to use it:  
`mount -t tmpfs varrun /var/run` or `mount -t tmpfs udev /dev` 

* Flash storage (EEPROM)
     * YAFFS – Yet Another Flash File System
     * JFFS / JFFS2 – Journaling Flash File System
     * UBIFS - Unsorted Block Image File System

#### Unix Filesystems Concepts

In Unix filesystems, files are represented by [inodes / i-nodes](https://unix.stackexchange.com/a/4403). These are structures that contain file descriptions (type, access right, owners, size, pointers) and are kept in memory by the kernel (open).  
Directories are special files ([dentry / d-entry lists](https://unix.stackexchange.com/a/4403)) and devices are accessed by I/O on special files.

Journaled Filesystems were designed to keep in working order after a sudden shutdown or crash. All changes are first described in the jornal before being commited to files (and then cleared).  
This also increases substantially the number of writes, that can reduce flash storage lifespan. Some workarounds are external journals or even no jornals.  

Virtual Filesystem is a abstraction which allows multiple filesystems to be supported simultaneously by the kernel.  
Mixing filesystems can be done using symbolic links `ln -s` or with something like UnionFS.  
To freely expand and shrink filesystems (usually sitting on a partition, being limited by disk size), it is used a "Virtual Volume Manager" that separates the physical composition of the storage devices from logical exposure.  

Swap space is RAM on disk, and so, it is much slower to access.


#### Raid (Redundant Array of Inexpensive Disks)

Can reduce latency by writing/reading in parallel, increase reliability by exploiting redundancy and can be implemented in hardware/software.
Types of Raid:
* Raid 0: Stripping data across discs (read/write in parallel but decreases reliability)
* Raid 1: Mirroring (Redundancy, reliability, potencially better read performance)
* Raid 3: Block Parity in extra disk
* Raid 4: Stripping + Block-level Parity
* Raid 5: Stripping + Block-level Distributed Parity
* Raid 10: (N Disks at Raid 1) doing Raid 0 with (another N Disks at Raid 1)

#### Adding a new disk

1. Install new hardware (Verify disk recognized by BIOS)
2. Boot (Verify device exists in /dev)
3. Partition (`fdisk /dev/sdb`)
4. Create filesystem (`mkfs –v –t ext3 /dev/sdb1`)
5. Add entry to /etc/fstab (`/dev/sdb1 /proj ext3 defaults 0 2`)
6. Mount new FS (`mount -a`)

#### Relevant Commands

##### [tar](https://www.ibm.com/docs/en/aix/7.1?topic=t-tar-command) (Tape archive)

Based on the old tape format, this command creates a archive, often called tarball, that contains a variety of files and directories highly compressed.  
To create a tar archive: `tar -cxf output_tarball input_directoryOrFile`  
To list files in a tar archive: `tar –tvf output_tarball`  
To extract files: `tar -xvf output_tarball`

##### [cpio](https://www.ibm.com/docs/en/aix/7.2?topic=c-cpio-command) (Copy in and out)

Copy a list of files into a large, single file. Uses headers to facilitate recovery.  
To create a cpio backup: `find ./directory_to_copy | cpio -ov > backup_file`  
To list files in a backup: `cpio -itv < backup_file`  
To extract files from a backup: `cpio -idv < backup_file`

##### List devices and partitions
`cat /proc/partitions`  
`lsblk`  
`fdisk -l`  

##### Filesystem Commands:

Reports the amount of available disk space used by mounted filesystems: `df`  
Check and Repair Filesystems with: `fsck`

##### [dd](https://man7.org/linux/man-pages/man1/dd.1.html)

Often called data duplicator, disk dump or even data destroyer, it is a powerful tool that can be used with files, devices, memory and even ports.
To use it to make a filesystem image: `dd if=/dev/sda1 of=mypart.img`  
Or to restore a filesystem: `dd if=mypart.img of=/dev/sda1`  
Copy physical memory to file using: `dd if=/dev/mem of=mymemory.bin bs=1k skip=412 count=43`  
(These are only examples, but this is one of the most powerful and dangerous tool)
