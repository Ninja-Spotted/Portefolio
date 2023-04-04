---
title: "FreeRTOS on Pi Pico"
parent: Raspberry Pi Pico
permalink: "/raspberrypi-pico/freeRTOS"
layout: default
---

### FreeRTOS

FreeRTOS is a open-source (MIT licence) Real-Time Operating System (RTOS) used in microcontrollers and small microprocessors that is very popular acording to the [website](https://www.freertos.org/RTOS.html). It aims to be reliable, accessible and easy to use.

A RTOS is basically an elevated task manager system that can do the management of different processes with full controll of the timing of their execution, switching tasks quite fast, which for the majority of cases nowadays, look like they are running concurrently. This happens because the [scheduler](https://www.freertos.org/implementation/a00005.html), which is also a task that runs with higher priority than the others, decides which task should be executed next. There are also other concepts, like [Queues, Mutexes, Semaphores](https://www.freertos.org/Embedded-RTOS-Queues.html) which deal with some shortcomings of using a system implemented like this.

##### Small note from me: I used it for the first time on one of my optional courses, where I developped programs using a STM32F103RBT6 development board with a hat with some other sensors and actuators, by first using the Cortex Standard Library and using the traditional C, and latter on using the FreeRTOS Kernel. From that experience I can say with confidence that you __should__ first learn and build some C programs before using the FreeRTOS Kernel, since most of the code under the hood came from my C programs (things such as clock speed setting, GPIO configuration and interruptions.  

#### Instalation of C/C++ SDK and FreeRTOS for the Pi Pico

