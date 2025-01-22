---
title: "Cpp"
parent: Learning
permalink: "/learning/cpp"
layout: default
---

# C++

## Introduction

TODO

## Things I found interesting

### Variable initialization

There are 5 common forms of initialization in C++ ([see here](https://www.learncpp.com/cpp-tutorial/variable-assignment-and-initialization/)):

    int a;         // default-initialization (no initializer)
    
    // Traditional initialization forms:
    int b = 5;     // copy-initialization (initial value after equals sign) --> Inherited from the C language
    int c ( 6 );   // direct-initialization (initial value in parenthesis)  --> Not a function! (Starts with a type)
                                                                                Also used when values are explicitly cast
    // Modern initialization forms (preferred):
    int d { 7 };   // direct-list-initialization (initial value in braces)  --> Disallows narrowing conversions
                                                                                (Only when initializing)
    int e {};      // value-initialization (empty braces)                  -- zero-initialization to value 0
                                                                              (Or closest to zero for the type)

As of C++17, the first 3 behave identically in most cases.
A significant difference is that direct-list-initialization disallows narrowing conversion:

    int w1 { 4.5 }; // compile error: list-init does not allow narrowing conversion

    int w2 = 4.5;   // compiles: w2 copy-initialized to value 4
    int w3 (4.5);   // compiles: w3 direct-initialized to value 4

### Usage of `std::endl` vs `\n` ([see here](https://www.learncpp.com/cpp-tutorial/introduction-to-iostream-cout-cin-and-endl/)):

`std::endl` is necessary to indicate that a line of output is a complete thought (and is not completed in another output line somewhere in the code), as well as positioning the cursor on the next line, making them appear where expected.  

However, `std::endl` is often inefficient, since it outputs a newline and flushes the buffer (which is slow). Prefer `\n` over `std::endl` when outputting text to the console. When outputting text to the console, we typically don’t need to explicitly flush the buffer ourselves. C++’s output system is designed to self-flush periodically, and it’s both simpler and more efficient to let it flush itself.

    std::cout << "x is equal to: " << x << std::endl;                          --> May not be necessary to flush

    std::cout << "x is equal to: " << x << '\n'; // single quoted (by itself)  --> Prefered way
    
### Input more than one number at once ([see here](https://www.learncpp.com/cpp-tutorial/introduction-to-iostream-cout-cin-and-endl/))::

    std::cout << "Enter two numbers separated by a space: ";

    int x{}; // define variable x to hold user input (and value-initialize it)
    int y{}; // define variable y to hold user input (and value-initialize it)
    std::cin >> x >> y; // get two numbers and store in variable x and y respectively

    std::cout << "You entered " << x << " and " << y << '\n';

If only a number is entered, the next input of the buffer will be used to fill the second variable.

### Function arguments

![image](https://github.com/user-attachments/assets/4d8d899c-ff7d-4668-9143-8fd576f81d0b)

https://www.youtube.com/watch?v=B_4x7WlQr7M <- good video to watch
