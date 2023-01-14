---
title: "Boot"
parent: Computer Architecture
permalink: "/computer_architecture/boot"
layout: default
---

## Processors

### 8086

* 16 Bit Registers
* 16 Bit Data Buses
* 20 Bit Address Buses (2^20 = 1 MiB Addressable Memory)

#### Registers

* AX-DX: General Registers
* SI, DI: Index Registers
* BP, SP: Pointer Registers
* Flag Registers
* CS, DS, SS, ES: Segment Registers
    * Code Segment (CS): implicit in all fetch instructions.
    * Data Segment (DS): implicit in remaining data access operations in memory.
    * Stack Segment (SS): implicit in stack operations (push, pop) and indirect addressing.
    * Extra Segment (ES): explicit selection to access data in memory.
    
Imediate Addressing: MOV AL, #13  
Direct Addressing: MOV DX,[1234h]  
Indirect Addressing: MOV AL,[BX]  

#### DMR (Direct Memory Access)

Implements data transfers between memory-devices without CPU time.
Different Configurations:
* Single Bus, detached DMA controller (2 bus cicles)
* Single Bus, integrated DMA controller (1 bus cicle)
* Independent bus (1 I/O bus cicle and 1 memory bus cicle)
