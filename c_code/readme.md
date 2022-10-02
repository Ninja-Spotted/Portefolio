---
title: "C Programming"
permalink: "/c_code"
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

These files with the `.so` extensiozzzn are are dynamically linked shared object libraries and can be obtained using `cc -o libfile.so -shared ofile1.o ofile2.o`.
\
After that, `ldconfig` can be used to create the necessary links and cache to the most recent shared libraries found in the directories specified on the command line.
\
`cc -o executable ofile1.o ofile2.o -Llibdir -lexampleso` (where exampleso refers to the file `exampleso.so` and libdir being the library directory) will generate a executable that **loads the library in the start of the application**:

- Smaller Size Executables
- Shared code on different executables
- Executables dependent on installed libraries
