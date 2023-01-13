---
title: "Kernel"
parent: Computer Architecture
permalink: "/computer_architecture/kernel"
layout: default
---

### Kernel

It was created as a hobby by Linus Torvalds, developed in C language and with a modular architecture.  
Being the biggest open-source project it means that it features key features like security, stability and portability.

#### System Calls
Main interface between the kernel and userspace. They provide the main kernel services like file/device and networking operations, communication between processes, memory mapping, timers, threads, etc.  
These calls are wrapped by the C library, so that applications never do system calls directly.

#### System and Kernel Information
Provided via virtual filesystems (/proc and /sys).

#### Versions
##### Linux 2.y
Versions are numerated with x.y.z.
* x.y : Major version
* z : Minor version
If y is even, that version is considered stable. If it is a odd number it is a development version.
##### Linux 3.x
Official kernel named 3.x, and stable versions are named 3.x.y.

#### Compilation
To compile linux:
1. Get it from the source at [kernel.org](https://kernel.org/).
2. Unpack and decompress the file.
3. Configure with `make xconfig` or `make menuconfig` or `make config`.
4. Compile the kernel with `make`.

#### Size
Most of the size of the source is consequence of the thousands of device drivers, network protocols, architecture support and filesystems.  
The core (scheduler, memory management, etc) is pretty small.

### Configuration
The configuration file is stored at the root of the sources, and should be edited with the tools previously mentioned.  
Some options can be compiled as modules (separated files) or statically into the kernel.  

`make oldconfig` can be used to upgrade a .config file from a earlier kernel.
`make allnoconfig` only enables the strongly recommended settings, leaving all other unselected. Typically used for embedded systems.
