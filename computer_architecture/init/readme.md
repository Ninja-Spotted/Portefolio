---
title: "Init"
parent: Computer Architecture
permalink: "/computer_architecture/init"
layout: default
---

### Init
[source](https://developer.ibm.com/articles/l-linuxboot/)  
The first program that is called which was compiled with the standard C library after the kernel boots. Usually it is locatted in `sbin/init` but it can also be in other places as a simple shell script.

#### Init Process
It is a process of the system, with PID=1, being the parent to all processes.

* inittab file:  
Used to define the initial runlevel (software configuration to allow only a selected group of processes to exist). Both GRUB and LILO can change runlevel at boot time.

* init.d:  
This is a directory that can be used to start/stop individual daemons (background processes).

* /etc/rc.d:  
Contains scripts to used to control the starting, stopping and restarting of daemons. scripts starting with K will run first and kill the associated processes, while those starting with S will start them

* chkconfig:  
Command used to configure services on/off and add/remove them from runlevels.

#### systemd Process
It another process of the system, with PID=1, being the parent to all processes. It is becoming more prevalent and is mostly compatible with init.

* /etc/systemd/system/:  
Everything is in this directory, with lots of symbolic links to startup files.  
Main Commands: `systemctl` and `journalctl`.

* Targets instead of Runlevels
Runlevels may still exist as symbolic links to new targets
* Works on units  
Are different services, sockets, targets, devices, mount, snapshots. Mosly services.

* systemclt used to enable or disable units.
