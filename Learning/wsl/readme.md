---
title: "Windows Subsystem for Linux"
parent: Learning
permalink: "/learning/wsl"
layout: default
---


## Windows Subsystem for Linux

The [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/) is a compatibility layer (interface that allows binaries for another system to run on a host system by translating the system calls into native ones) for running Linux binary executables natively on Windows.

### Instalation

To use this tool you must be running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11 as stated in the [official documentation](https://docs.microsoft.com/en-us/windows/wsl/install). Then, you can use `wsl --install` in *administrator* Powershell or Command Prompt to install everything
You can install multiple distros under WSL and run them at the same time.  

### Usage

#### Installing a new distribution
Use `wsl --install -d <Distribution Name>` to install a distribution.  
See which distributions are available through the online store with `wsl --list --online`. It is also possible to [import any distro](https://docs.microsoft.com/en-us/windows/wsl/use-custom-distro) using a TAR file. For future reference, this is how you can [create a custom distro](https://github.com/Microsoft/WSL-DistroLauncher).

#### Managing existing distributions
With `wsl -l -v` you can list the installed linux distributions, as well as the version of WSL of each one of them.  
The `wsl --setdefault <DistributionName>` command allows changing the default distro used when executing commands in the Powershell.  
To run a specific distro without changing the default, use `wsl -d <DistributionName>`, type the distribution's name or click the icon on the Windows Start Panel.  
Shutdown gracefully a distribution by using `wsl -t DISTRO-NAME` after `wsl -l -v`.  
Shutdown **All** distributions installed using `wsl --shutdown`.
