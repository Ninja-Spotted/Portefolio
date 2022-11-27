---
title: "Filesystems"
parent: Computer Architecture
permalink: "/computer_architecture/filesystems"
layout: default
---

### Filesystems

A version control system (VCS) is a software tool used to track and manage changes to a filesystem, often used in collaborative work.  
Nowadays, one of the most used VCS is Git, used via remote repositories like GitHub, GitLab or BitBucket.

#### Relevant History

Physical disk media history has much effect on everyday since many concepts storage still use vocabulary related to disks.
![Disk](https://images.wondershare.com/recoverit/article/2019/12/sector-track-image.jpg)  
For example:
- Sector: containing 512 bytes.
- Cluster: aka allocation unit, it consists of one or more sectors and represents the minimum amount of space that an operating system allocates for saving a file.

It is possible to check the information about a disk using `hdparm -i /dev/your_disk`. Use `lsblk` to get a list of partitions and disks the system.

#### Disk Devices and Booting

[source](https://tldp.org/HOWTO/Unix-and-Internet-Fundamentals-HOWTO/bootup.html)  
Usually, when a computer is turned on

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
