---
title: "Rust"
permalink: "/rust"
layout: default
---

[PDF](/Portefolio/SISTCA_2021-22_3DG_Grupo4_Rust.pdf)

## Rust
Rust is hard, but it can also be a great experience to anyone that finds the time to try and learn: Check out [Rust](https://www.rust-lang.org/).  
It was launched in 2012 in collaboration with Mozilla, and its goal is to make possible to build reliable and efficient system software.  
Rust is used by developers on networking software, for example, web servers, mail servers and web browsers. Furthermore, you can use it for game development, web-assembly programs, applications for embedded devices and command line programs. It is also present in compilers, interpreters, databases, operating systems and cryptography.  
\
One of the big advantages of rust is providing memory safety and correcting many bugs related with it's incorrect use in languages like C and C++. Another big advantage is it's ability to process large chunks of data.  
\
Rust is one of the most diversified languages to learn and start using to replace bloated code on other applications. Since 2018, the community around Rust has been improving the experience on various domains, such as CLI (Command Line Interface) Tools, WebAssembly, Networking and even Embedded devices with necessities for low-level control, developing various crates and guides to make the experience smoother.  
That means you can use the same language to build the structure to a database accessible on the web, program microcontrollers, and even build your cross-platform programs. If you are interested, you can also use rust to build your own kernel, with bare metal support for the hardware.  
\
It’s important to note that Rust is also the [most loved language](https://insights.stackoverflow.com/survey/2021#section-most-loved-dreaded-and-wanted-programming-scripting-and-markup-languages) for the sixth-year according to the annual survey from Stack Overflow, but despite that, Rust is not yet among the five most used programming languages, since the learning curve can be quite stiff.  
\
The objective of this document is to present an introduction to the Rust language and some of it's applications.

### Important features
There is a few important concepts around the Rust Language that one should be aware of, for example, the Ownership feature, which makes Rust to be memory safe without needs for a garbage collector. It is Rust most unique feature, and, in contrary to other languages, with garbage collections or explicit need to allocate and free memory, Rust uses a set of rules that the compiler checks, and, if any are violated, the program won’t compile. On the positive side, it won’t slow down your program while running.  
\
Traits allow type classes to adopt different behaviors, inspired by the Haskell language. Basically, floats and integers can both implement the ‘Add’ trait and any type that can be printed implement the ‘Display’ or ‘Debug’ traits.  
\
There are also Macros, like ‘println!’ that can take form of function calls but operate on distinct terms, it can take various numbers of parameters and can implement traits before compilation. The main downside, is that you need to write more complex code, and you must define macros or have them called before using them, whether functions can be defined and called anywhere.

### Setup and Installation
To get started with Rust, the first thing you should do is to go to the [official website](https://www.rust-lang.org/) and head to the “Getting Started” page. Here you can choose to install Rust through the tool called Rustup, which is supported on various systems and arquitectures, but for our convenience it will only show the version recommended for your system. During the installation it will advise to install the Visual C++ prerequisites on Windows from the link provided. Follow the instructions and continue with the installation.
There is another prompt to see if the user wants to change directory of installation but it’s recommended to use the default settings.
After this step, Rust is installed on the system. To confirm this, just write in the console "rustc --version" and check if a prompt gets launched.

    C:\Users\NinjaChomp>rustc --version
    rustc 1.59.0 (9d1b2106e 2022-02-23)

If the output was different, you may need to restart the shell for the changes to occur.
It is also advisable to install a IDE like [Visual Studio Code](https://code.visualstudio.com/) or [VSCodium](https://vscodium.com/) where you can install extensions for many languages and helps with code completion and highlights, but you can use a text editor like [Notepad++](https://notepad-plus-plus.org/downloads/), or the default on your system. For reference, in this guide we will be using Visual Studio Code, but VSCodium should have the same instructions.

### First steps (Hello, world!)
Now that we are in conditions of starting programming, open up VS Code and start by choosing a folder in system where the files will be placed (File -> Open Folder) and start by opening the built-in terminal and type 'cargo new hello'. This will create a new folder with the necessary files. Using the sidebar file explorer, navigate to hello/src/main.rs and open it. As you can see, the default file is already ready with the “Hello, world" ready to be printed in the terminal. To do this, navigate in the terminal to the hello folder (using 'cd hello') and then do 'cargo run'.  
If everything works as intended, an “Hello, world!” was printed in the terminal!

        PS C:\Users\NinjaChomp\Documents> cd hello
        PS C:\Users\NinjaChomp\Documents\hello> cargo run
            Finished dev [unoptimized + debuginfo] target(s) in 0.01s
            Running `target\debug\hello.exe`
        Hello, world!
        PS C:\Users\NinjaChomp\Documents\hello>

Also, if you pay close attencion to the output of the terminal, you can see that the program was made into an executable file and it can be executed even with a double click (but you won’t see this message unless you execute it on a command line!).

### Example of Rust Exercises
1. Numbers of Armstrong
3. Volume of Solids
4. ??

### TO DO (Sintaxe)


