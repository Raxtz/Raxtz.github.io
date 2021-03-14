---
layout:     post
title:      计算机组成原理—Chapter 2 Computer Evolution and Performance
subtitle:   计组碎碎念
date:       2021-03-14
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 计组
---

- The evolution of computers has been characterized by
  - increasing processor speed,
  - decreasing component size,
  - increasing memory size,
  - and increasing I/O capacity and speed.
- **Factors responsible for increasing processor speed**
  One factor responsible for the great increase in processor speed is the shrinking size of microprocessor components; this reduces the distance between components and hence increases speed.
  However, the true gains in speed in recent years have come from the organization of the processor, including
  heavy use of pipelining and parallel execution techniques and 
  the use of speculative execution techniques.
  All of these techniques are designed to keep the processor busy as much of the time as possible.
- **Balancing the performance of the various elements**
  Processor speed has increased more rapidly than memory access time.
  Compensate for this mismatch: caches, wider data paths from memory to processor, more intelligent memory chips



## 2.1 A Brief History of Computers

### The First Generation: Vacuum Tubes (1946-1957)

- Vacuum Tubes
- Von Neumann Machine
- Commercial computer



#### ENIAC

Electronic Numerical Integrator And Computer

Mauchly (EE professor) and Eckert (grad student), University of Pennsylvania

the world's first general-purpose electronic digital computer (decimal arithmetic)

started 1943, finished 1946, used until 1955

很大，没办法存数据和程序



#### Von Neumann / Turing

Stored-program concept (John von Neumann, 1945)

- Data and instruction encoded in binary
- Data and instruction stored in same memory
- Can change program without rewriting



1946, von Neumann began the design of new stored-program computer

At the Princeton Institute for Advanced Studies, referred as IAS

completed in 1952

IAS is the prototypes of all subsequent general-purpose computers



The general structure of the IAS computer:

- A main memory, which stores both data and instructions
- An arithmetic and logic unit (ALU) capable of operating on binary data
- A control unit, which interprets the instructions in memory and causes them to be executed
- Input and output (I/O) equipment operated by the control unit

With rare exceptions, all of today's computers have this same general structure and function and are thus referred to as **von Neumann machines**.

##### IAS memory

The memory of the IAS consists of 1000 storage locations, called *words*, of 40 binary digits (bits) each.

Each number is represented by a sign bit and a 39-bit value. (number word)

A word may also contain two 20-bit instructions, with each instruction consisting of an 8-bit operation code (opcode) specifying the operation to be performed and a 12-bit address designating one of the words in memory (numbered from 0 to 999). (instruction word)

##### IAS register

CU get the instruction from memory and execute one at a time.

Both the control unit and the ALU contain storage locations, called *registers*, defined as follows:

- Memory Buffer Register (MBR)
  Contains a word to be stored in memory or sent to the I/O unit, or is used to receive a word from memory or from the I/O unit.
- Memory Address Register (MAR)
  Specifies the address in memory of the word to be written from or read into the MBR.
- Instruction Register (IR)
  Contains the 8-bit opcode instruction being executed.
- Instruction Buffer Register (IBR)
  Employed to hold temporarily the right-hand instruction from a word in memory.
- Program Counter (PC)
  Contains the address of the next instruction-pair to be fetched from memory.
- Accumulator (AC) and Multiplier Quotient (MQ)
  Employed to hold temporarily operands and results of ALU operations.

##### IAS instruction cycle -- two subcycles

1. fetch cycle
2. execute cycle



#### Commercial Computer

UNIVAC I

UNIVAC II

IBM



### The Second Generation: Transistors (1958-1964)

- High level languages
- Floating point arithmetic
- System software



### The Third Generation: Integrated Circuits (1965-1971)

- Discrete Component
  - Electronic equipment <-- largely of discrete components
- microelectronics
  - A computer <-- gates, memory cells and interconnections
  - 8-inch wafer
    Each grid on the wafer can be divided as a chip
    Chip can be interconnected to large circuit
- Moore's Law
  - Number of transistors on a chip will double every year
  - Pace slowed to doubling 18 months since 1970's
- IBM 360 series
  - 1964, IBM announced the System/360.
  - Replaced (& not compatible with) 7000 series
  - First planned "family" of computers
    - Similar or identical instruction set
    - Similar or identical operating system
    - Increasing speed
    - Increasing  number of I/O ports
    - Increasing memory size
    - Increasing cost
- DEC PDP-8
  - 1963, DEC inc, First minicomputer
  - Did not need air conditioned room
  - Small enough to sit on a lab bench
  - $16,000, low cost
    - $100k+ for IBM 360
  - Embedded applications
    - Original Equipment Manufacturers (OEM) -- Resale it
  - **Bus structure**



### Later Generation

- Less agreement to define this generation
- LSI, VLSI, ULSI(ultra-large-scale integration)
- Two most results of technology change

#### Later generation: Semiconductor Memory (1970)

1960s, memory-constructed from tiny rings of ferromagnetic material, expensive, bulky, destructive readout (优点：恢复数据较简单)

1970 Fairchild, semiconductor memory

- Chip, Size of a single core, holds 256 bits
- Non-destructive read, much faster
- Capacity approximately doubles each year
- (缺点：恢复数据较困难)

#### Later generation: Microprocessors -- Intel (1971)

Robert Noyce and Gordon Moore, leave Fairchild, co-founded Intel in 1968

Intel (the abbreviation for Integrated Electronic)

- 1971-4004
  - First microprocessor
  - All CPU components on a single chip
  - 4 bit (Data Bus Width)
  - Designed for specific applications

- Followed in 1972 by 8008
  - 8 bit
  - Designed for specific applications
- 1974 - 8080
  - Intel's first general purpose microprocessor
- End of 1970s
  - 16-bit general purpose, 8086
  - 1985, 32-bit, 80386



## 2.2 Designing for Performance

### Improvement in Chip Organization and Architecture

#### Approaches to Increase Processor Speed

- Increase hardware speed of processor
  - Shrinking logic gate size
    - More gates, packed more tightly
    - Propagation time for signals is reduced
- Increase the size of speed of caches
  - Dedicating part of processor chip to cache
    - Cache access times drop significantly
- Change processor organization and architecture
  - Increase effective speed of execution
  - Involve parallelism

#### Problems: Clock Speed and Login Density

- Power
  - Power density increases with density of logic and clock speed
  - Dissipating heat
- RC delay
  - Wire interconnects thinner, increasing resistance
  - Wires closer together, increasing capacitance
- Memory latency
  - Memory speed lag process speed



### In Recent Years, Two Main Strategies

#### Increased Cache Capacity

- Typically two or three levels of cache between processor and main memory
- Chip density increased
  - More cache memory on chip
    - Faster cache access
- Pentium chip devoted about 10% of chip area to cache
- Pentium 4 devotes about 50%

#### New Approach -- Multiple Cores

- Multiple processors on single chip
  - Large shared cache
- If software can use multiple processors, doubling number of processers almost doubles performance
- Large caches are justified due to the less power consumption
- First commercial multi-processor, IBM POWER4

