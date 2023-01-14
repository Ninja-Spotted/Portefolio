---
title: "Loadable Kernel Modules"
parent: Computer Architecture
permalink: "/computer_architecture/lkm"
layout: default
---

### Loadable Kernel Modules

#### Commands
* `lsmod` or `cat /proc/modules` to list **loaded modules**.
* `insmod module.ko` or `modprobe modulo` to insert a new module.
* `rmmod module` to remove a module.
* `modinfo module` to obtain information about the module.
* `ksysm` or `cat /proc/ksyms` to list symbols provided by kernel.

#### Hello Module (Example)

        /* hello.c */
        #include <linux/init.h>
        #include <linux/module.h>
        #include <linux/kernel.h>
        static int __init hello_init(void)
        {
        printk(KERN_ALERT "Good morrow");
        printk(KERN_ALERT "to this fair assembly.\n");
        return 0;
        }
        static void __exit hello_exit(void)
        {
        printk(KERN_ALERT "Alas, poor world, what treasure");
        printk(KERN_ALERT "hast thou lost!\n");
        }
        module_init(hello_init);
        module_exit(hello_exit);
        MODULE_LICENSE("GPL");
        MODULE_DESCRIPTION("Greeting module");
        MODULE_AUTHOR("William Shakespeare");
        
* `__init`: Executed on module load. Removed after initialization (static kernel or module).
* `__exit`: Executed on module unload. It is discarded when compiled statically.

Execution:

        # modprobe hello
        Good morrow to this fair assembly.
        # lsmod
        ...
        hello
        ...
        # rmmod hello
        Alas, poor world, what treasure hast thou lost
        
##### Module explanations:
Headers are specific to the Linux Kernel `<linux/xxx.h` since there is no access to the usual C library.  
There is an initialization function (`modulename_init()`), called when module is loaded.  
A cleanup function (`modulename_exit()`) called when module is unloaded.  
Other functions can be used for metadata informations (MODULE_LICENSE(),
MODULE_DESCRIPTION() and MODULE_AUTHOR()).  

Symbols can be exported to modules using `EXPORT_SYMBOL(symbolname)` which exports a variable or function to all modules. **A normal driver should not need any non-exported function**.

##### Compiling a module
* Out of tree: Code outside the kernel source tree, where it might be easier to handle modifications than to the kernel itself however, it is not integrated into the kernel and cannot be build statically.
* Inside the tree: Can be integrated in the kernel configuration/compilation and built statically if needed.

Example of compilation outside the tree:

    ifneq ($(KERNELRELEASE),)
    obj-m := hello.o
    else
    KDIR := /path/to/kernel/sources
    all:
        $(MAKE) -C $(KDIR) M=`pwd` modules
    endif

KDIR is either full kernel source or just kernel headers directory. A kernel module compiled against version X of kernel headers will not work on kernel version Y.

##### Module Parameter
These work kinda as function parameters that can be set when loading the module.


#### Creating a character driver

* User-space needs: Name of a device file in /dev to interact with the device driver (open, read, write, close).
* Kernel needs: Know which driver is in charge of device files with major / minor number pair.  
  For a driver to have handlers to execute when user-space performs operations.
  
`mknod /dev/name c major minor` Can be used to create a dentry and corresponding inode for special file.
  
Steps:
1. Initializing: Register the driver with major / minor numbers and callback functions for file operations.
2. In the read callback: Send data to userspace aplication with `copy_to_user()`.
3. In the write callback: Read data from userspace aplication with `copy_from_user()`.

The kernel represents character drivers with the cdev structure.  
Declaring it globally within the module: 

      #include <linux/cdev.h>
      static struct cdev acme_cdev;

In the init function:

      cdev_init(&acme_cdev, &acme_fops);
      cdev_add(&acme_cdev, acme_dev, acme_count);

##### read()

Called when user-space uses the read() system call on the device file. It must read data from the device, returning the number of bytes read.

##### write()
Called when user-space uses the write() system call on the device. Must read at most sz bytes from buf, write it to the device, update off and return the number of bytes written.


#### Exchanging data with user-space

Kernel code is not allowed to directly access user-space memory. There are special functions:  
* For a single value:
    * `get_user(v,p)`: The kernel variable v gets the value pointed by the user-space pointer p.
    * `put_user(v,p)`: Value pointed by the user-space pointer p is set with the content of kernel variable v.
* For a buffer:
    * `copy_to_user` and `copy_from_user`.
        
### Kernel and device drivers

Many device drivers are not implemented directly as character drivers, they are implemented under a "framework".  
They rely on the "bus infrastructure" (USB, PCI, SPI, etc.) to enumerate and communicate with them.

