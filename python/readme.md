---
title: "Python"
permalink: "/python"
layout: default
---


## Python

Python is one of the most widely adopted programming languages being one of the most interesting and the third most popular language. It is an interpreted language, which means that it can execute instructions directly and freely, without compiling the code previously into low-level machine instructions. Being a general-purpouse language, it means it can be used in a wide variety of application domains.

### Instalation

Most Linux Distributions come with Python pre-installed. To confirm this you can write `python3` in terminal and check if a prompt gets launched. If not, you can install it doing `sudo apt install python3` on Debian based distributions.  
\
It is also recommended to use a code editor such as Visual Studio Code to use functionalities built into it like Auto-complete and debugging.

### Use

To make a Python file, just make a new file with the extension `.py`. Open it and start programming. To run the code you can type in the terminal `python nameoffile.py`.

### Data Structures and Variables

As in many programming languages, there are many types of ways of organizing data. There are 2 types of data structures:  

* Linear data structures (Organized linearly, one after another, only one item can be acessed at a time):
    * Array
    * Linked list
    * Queue
    * Stack  
* Non-linear data structures (Not organized in sequential order, but are connected to several other data items to represent relationships):
    * Tree
    * Heap
    * Hash Table
    * Graph

There are also 5 standard data types that self-define the operations and storage methods:
* Numbers (3 types: int, float, complex)
* Strings (with `""` or `''`, allow parts of strings to be taken with `[index]` with indexes going from 0 to lenght-1. There are also useful methods to use with strings) 
* Lists (`['apple', 'banana', 'cherry']`, can be acessed same as Strings but can use other functions that add value to it)
* Tuples (Same as list but with `('apple','banana')` and you cannot update them)
* Dictionaries  (Unordered, updatable and indexed. It's Python mapping type. **Look like Structs**)

To create a variable you don't need to declare variables before using them, or even declare their type. Every variable is an object created at the moment a value is assigned to it. To assign values the `=` is used. There are some rules for variable creation:
* You must start the name of variable with a letter or underscore character
* Can only contain alpha-numeric and underscores
* Variable names are case-sensitive, which means `Result`, `RESULT` and `result` are three different variables.  
\
You can assign values to multiple variables simultaneously, for instance:  
`a=b=1` or `a, b, c = 1, 2, "result"`  

### Input and Output 

Taking input from the user is very simple. The `input()` function takes input after printing the statement in the function parameter. It can then be saved in a variable and printed out.  
\
The most used statement to output variables is `print()`. You can combine text and variables. By using the `+` operator you can combine variables like text however if you use it with numbers it works as an operator.

            x = input ("Enter your name: ")
            print("Hello, " + x)

### Conditions and Iterations

Conditions can be expressed in Python using 3 keywords: `if`, `elif` and `else`:

            a = 200
            b = 33
            if b > a:
               print("b is greater than a")
            elif a == b:
               print("a and b are equal")
            else:
               print("a is greater than b")

Iterations are pieces of code that execute instructions until a condition is met or infinetely. You can also nest loops inside another.
##### For Loop (Definitive iteration):
            for x in fruits:
               print(x)

##### While Loop (Indefinitive iteration)
            while i < 6:
               print(i)
               i += 1

The `break` statement can be used to exit a loop at an early stage.

### Functions

A function is a sequence of code commands that is used for a particular task. To define a function, Python uses `def`. Then, to execute it, just call its name:

            def my_function():
               print("Hello from a function")
               
            my_function()
            
### Modules

We can extend the functionalities of Python using Modules. They are code libraries that contain extra functions like for date and time. To use modules you use the `import` keyword:

            inport datetime
            x = datetime.datetime.now()
            print(x)

### Classes and Methods

Classes are a object-oriented programming blueprints to create objects using the keyword `class`. It will contain attributes that can be acceced with the dot (.) operator.  
\
All classes **should** have a function called __init__(), that allows it to create instances of this class and assign values. It is automatically executed when an instance of the class is initialized:

            class Person:
               def __init__(self, name, age):
                  self.name = name
                  self.age = age
            
            p1 = Person ("John", 36)
            print(p1.name)
            print(p1.age)
            
Methods are quite similar to functions. The main difference is that a method is  called on an object, and a function is not. That means a method can change the state of an object but a function can only operate on it, not change it.

            def mymethod(self):
               print("Hello my name is " + self.name)
