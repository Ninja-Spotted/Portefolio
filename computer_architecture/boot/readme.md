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

#### Boot Firmware

* Bios  
Boot firmware present in every PC from the last 25 years and mainly used for compatibility reasons. It is difficult to support for new devices and implementations are not consistent.

* EFI  
Designed as a BIOS replacement, running in native processor mode and can be programmed in C/C++. Well documented and modular/extensible.

* UEFI (Unified EFI)  
Defines secure boot (Optional mode to allow booting only signed OS) and a shell environment, with specific support for 32-bit and 64-bit OS.

##### UEFI Booting
1. Boot Manager checks boot configuration.
2. Required drivers may be loaded.
3. EFI System Partition (ESP) is selected.
4. The FAT filesystem from ESP is mounted as /.
5. The file `/EFI/BOOT/BOOT<xxx>.EFI` is used as OS loader.
6. OS loader is loaded and run.


#### Boot Process
* Stage 1 (MBR)

The primary bootloader that resides in the MBR code contains program code and a small partition table. It serves to find and load the secondary boot loader (stage 2) from an active partition. When this happens, that partition boot record is read into RAM and executed.

![](https://developer.ibm.com/developer/default/articles/l-linuxboot/images/fig2.gif)

* Stage 2 (GRUB, LILO, Syslinux)

The secondary bootloader (also commonly called kernel loader) aims to load the Linux Kernel and optional initial RAM disk.

#### GRUB
GRUB is an OS independant boot loader with flexible command line interface, filesystem access and support for multiple executable formats. It can support diskless systems, download OS from network and more.

##### GRUB Boot Process
1. BIOS finds and transfers control to the MBR of a bootable device
2. MBR contains GRUB Stage 1 (That just loads the next stage due to the small size of MBR).
3. Stage 1.5, located following the MBR loads Stage 2.
4. Stage 2 displays to the user the boot menu (to manually specify boot parameters).
5. GRUB loads the kernel into memory and passes control.

#### LILO
LILO is a bootloader not dependent on a specific filesystem and can have up to 16 images.

#### Syslinux
Syslinux uses FAT partitions and has instalation programs for Windows and Linux.

* Kernel
During the boot of the kernel, the initial-RAM disk (initrd) that was loaded into memory by the stage 2 boot loader is copied into RAM and mounted. This initrd serves as a temporary root file system in RAM and allows the kernel to fully boot without having to mount any physical disks.


#### How are the modules inside a filesystem accessed when they are needed to support access to a filesystem?
Solution: RAM Disks.  
The bootloader passes the initrd image to kernel, loading both into memory. Then it passes the load address of the initrd image to the kernel before passing control to it.  

Other option is using the initramfs (Different implementation but same purposes.
