---
title: "Boot"
parent: Computer Architecture
permalink: "/computer_architecture/boot"
layout: default
---

### Boot


#### Disk Devices and Booting

[source](https://tldp.org/HOWTO/Unix-and-Internet-Fundamentals-HOWTO/bootup.html)  
Usually, when a computer is turned on it goes through a chip on the computer that runs the BIOS. This is a chip that points to a fixed place, usually the boot disk (lowest-numbered disk) and looks for a program called a bootloader, that has the function of starting the real operating system.  
It does it by looking for a kernel, loading it into memory. The reason for this multi-step process is because the BIOS is really basic, and can't access enough of the disk to load the kernel. Also, the bootloader allows the user to boot one of several OS from different places on the disk.  

##### Master Boot Record
[source](https://developer.ibm.com/articles/l-linuxboot/)  
The Master Boot Record (MBR) is the name given to the first sector of a disk. It contains information about the drive and identifies how and where the operating system is located.

* Stage 1

The primary bootloader that resides in the MBR code contains program code and a small partition table. It serves to find and load the secondary boot loader (stage 2) from an active partition. When this happens, that partition boot record is read into RAM and executed.

![](https://developer.ibm.com/developer/default/articles/l-linuxboot/images/fig2.gif)

* Stage 2

The secondary bootloader (also commonly called kernel loader) aims to load the Linux Kernel and optional initial RAM disk.
