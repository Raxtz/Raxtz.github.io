---
layout:     post
title:      计算机组成原理—Chapter 1 Introduction
subtitle:   计组碎碎念
date:       2021-03-05
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 计组
---


## 1.1 Organization and Architecture

**Computer architecture**: attributes that have a direct impact on the logical execution of a program

- the instruction set
- the number of bits used to represent various data types
- I/O mechanisms
- techniques for addressing memory

**Computer organization**: the operational units and their interconnections that realize the architecture specifications

- control signals
- bus width
- interfaces between the computer and peripherals
- the memory technology used

很多family产品，不更新architecture，只更新organization。
受众统一、软件通用。价格提高，性能提升。



## 1.2 Structure and Function

the hierarchical nature of complex systems

- a hierarchical system is a set of interrelated subsystems
- Each level of system hierarchy consists of set of components and their interrelationships.
- The behavior at each level depends only on a simplified, abstracted characterization of the system at the next lower level.

At each level, the designer is concerned with structure and function:

- **Structure**: The way in which the components are interrelated
- **Function**: The operation of each individual component as part of the structure

top-down approach



### Function

- Data processing
- Data storage
  - a short-term data storage
  - a long-term data storage
- Data movement
  - process: input-output(I/O), data communications
  - a directly connected device: a peripheral 
  - a remote device: communication lines
- Control



### Structure

Computer:

- **Central processing unit (CPU)** / **processor**: Controls the operation of the computer and performs its data processing functions.
- **Main memory**: Stores data.
- **I/O**: Moves data between the computer and its external environment.
- **System interconnection**: Some mechanism that provides for communication among CPU, main memory, and I/O. A common example of system interconnection is by means of a **system bus**, consisting of a number of conducting wires to which all the other components attach.



CPU:

- **Control unit**: Controls the operation of the CPU and hence the computer.
- **Arithmetic and logic unit (ALU)**: Performs the computer's data processing functions.
- **Registers**: Provides storage internal to the CPU.
- **CPU interconnection**: Some mechanism that provides for communication among the control unit, ALU, and registers.



Control Unit (a microprogrammed implementation):
operates by executing microinstructions that define the functionality of the control unit

- Sequencing logic
- Control memory
- Control unit registers and decoders





