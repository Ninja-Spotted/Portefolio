---
title: "C Programming"
permalink: "/c_code"
layout: default
---

### Libraries

In C and other languages, libraries are used to reutilize code in different applications and programs without having to write it on multiple source codes. This helps to reduce cluttering and avoiding changes on multiple files, helping with code maintenance and modularity.

#### Static Libraries

This files are recognized for the `.a` extention. They archive `.o` files
(as an example: `ar r libfile.a ofile1.o ofile2.o` will create an static library) which allows them to be linked when compiling the main program.

For example: `cc -o executable ofile1.o ofile2.o -Llibdir -l example` (where example refers to the file `libexample.a` and libdir being the library directory) will generate a executable with:

- Big size
- Repeated code on various executables
- Portable executables

