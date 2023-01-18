---
title: "C Libraries"
parent: Computer Architecture
permalink: "/computer_architecture/libraries"
layout: default
---

### Libraries

In C and other languages, libraries are used to reutilize code in different applications and programs without having to write it on multiple source codes. This helps to reduce cluttering and avoiding changes on multiple files, helping with code maintenance and modularity.

#### Static Libraries

These files are recognized for the `.a` extension. They archive `.o` files
(as an example: `ar r libfile.a ofile1.o ofile2.o` will create an static library) which allows them to be linked when compiling the main program.

For example: `cc -o executable ofile1.o ofile2.o -Llibdir -l example` (where example refers to the file `libexample.a` and libdir being the library directory) will generate a executable with:

- Big size
- Repeated code on various executables
- Portable executables

#### Shared Libraries

These files with the `.so` extension are are dynamically linked shared object libraries and can be obtained using `cc -o libfile.so -shared ofile1.o ofile2.o`.
\
After that, `ldconfig` can be used to create the necessary links and cache to the most recent shared libraries found in the directories specified on the command line.
\
`cc -o executable ofile1.o ofile2.o -Llibdir -l exampleso` (where exampleso refers to the file `exampleso.so` and libdir being the library directory) will generate a executable that **loads the library in the start of the application**:

- Smaller Size
- Shared code on different executables
- Executables dependent on installed libraries

#### Dynamic Linking/Loading

Dynamic Linking/Loading is the true intent of this kind of library. With it, we can load the dynamic shared object file (shared library) and keep the advantages of shared linking: shared memory across aplications, smaller program size and no need to bring out new versions of your program if one of the libraries gets updated. As an example:

        #include <stdio.h>
        #include <dlfcn.h>
        main()
        {
          int a=12;
          int b=6;
          int c;
          void *handle;
          int (*fsum)(int,int);
          handle = dlopen ("libsum.so", RTLD_LAZY);   // Loads the library
          fsoma = dlsym(handle, "sum");               // Obtain pointer to symbol
          c = (*fsum)(a,b);                           // Using pointed object
          dlclose(handle);                            // Freeing library
          printf("%d + %d = %d\n", a, b, c);
        }

#### Pratic Terminal Command Lines

- nm : Lists symbols from object files
- objdump : Displays information about object files (such as assembly form)
- ls -l : Lists the names of the files in directory along with the permissions, date, time and size
- grep : Can be used in conjunction with other commands to filter content from their outputs
