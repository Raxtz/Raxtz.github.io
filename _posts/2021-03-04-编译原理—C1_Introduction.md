---
layout:     post
title:      编译原理—Chapter 1 Introduction
subtitle:   龙书碎碎念
date:       2021-03-04
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 编译原理
---

Compilers: do the translation

## 1.1 Language Processors

1. compilers（一对一转换）

   source program --> target program

2. interpreters（一对多实现）

   source program + input(data)  --> output

在不修改原程序的情况下，用target program运行比用interpreter快；但interpreter因为一句一句运行，可以更好地找到错误。

Java language processors： compilation + interpretation （bytecodes, JVM）

![FPTGOR[)5H91X2H_H9I4H)7](C:\Users\62489\Desktop\FPTGOR[)5H91X2H_H9I4H)7.png)

- Preprocessor: a program to collect the source program which is divided into modules stored in separate files.

- Assembler: process the assembly language to produce relocatable machine code.

  大程序通常会被分片编译，所以machine code要靠后期连接起来

- Linker: resolve external memory addresses, where the code in one file may refer to a location in another file.

- Loader: put together all of the executable object files into memory for execution.



## 1.2 The Structure of a Compiler

Two parts:

- Analysis
- Synthesis

Analysis (front end)

- Input: source program; 
  output: an intermediate representation & a symbol table. (to the synthesis part)

- 把source program分成片，并impose a grammatical structure, 再用该structure创造个intermediate representation of the source program.
- 会报错，关于语法错误、语义错误
- 收集信息建一个a symbol table 

Synthesis (back end)

- Input: the intermediate representation & the symbol table;
  Output: target program



Phases:

- Lexical Analyzer
- Syntax Analyzer
- Semantic Analyzer
- Intermediate Code Generator
- (Machine-Independent Code Optimizer)
- Code Generator
- (Machine-Dependent Code Optimizer)

The symbol table is used by all phases.



### 1.2.1 Lexical Analysis

lexical analysis / scanning

Blanks separating hte lexemes would be discarded by the lexical analyzer.

For each lexeme, produce as output a **token** of the form 
**<token-name(, attribute-value)>** 
that it passes on to the syntax analysis.

- token-name: an abstract symbol
- attribute-value: points to an entry in the symbol table for this token

The symbol-table entry for an identifier holds information about the identifier, suchas its name and type.



### 1.2.2 Syntax Analysis

syntax analysis / parsing

The parser uses the first components of the tokens

a syntax tree



### 1.2.3 Semantic Analysis

The semantic analyzer uses the syntax tree & the symbol table

gathers type information and saves it in either the syntax tree or the symbol table, for subsequent use during intermediate-code generation

**type checking**

**coercions**



### 1.2.4 Intermediate Code Generation

two important properties:

- easy to produce
- easy to translate into the target machine

**three-address code**

	1. Each three-address assignment instruction has at most one operator on the right side.
	2. The compiler must generate a temporary name to hold the value computed by a three-address instruction.
	3. Some "three-address instructions" have fewer than three operands.



### 1.2.5 Code Optimization



### 1.2.6 Code Generation

Storage-allocation decisions are made either during intermediate code generation or during coe generation.



### 1.2.7 Symbol-Table Management

a data structure containing a record for each variable name, with fields for the attributes of the name.

Requirements:

- find the record for each name quickly
- store or retrieve data from that record quickly



### 1.2.8 The Grouping of Phases into Passes

Activities from several phases may be grouped together into a pass taht reads an input file and writes an output file.

compiler collections



### 1.2.9 Compiler-Construction Tools



## Other Things

### Auxiliary Components of Compiler Phases

**The literal table**

- Usage of Literal Table
  Literal table stores constants and strings used in a program
- Purpose of Literal Table
  The literal table is important in reducing the size of a program in memory by allowing the reuse of constants and strings

**The Symbol Table**

- Usage of Symbol Table
  Symbol table keeps information associated to identifiers: function, variable, constant and data type identifiers
- Symbol Table with Compiler Phases
  - Scanner,parser or semantic analyzer may enter identifiers and information into the table
  - The optimization and code generation will use the information provide by the symbol table

**Error handler**

- Errors can be detected during almost every compiler phase
- Error handler must generate meaningful error message and resume compilation after each error



### Realization of compiler structure

- Compiler may repeat one or more passes before generating target code
- Definition of Pass
  A pass is to process of  the entire source program or its intermediate representation one time

- A typical arrangement is one pass for scanning and parsing, one pass for semantic analysis and source-level optimization, and a third pass for code generation and target level optimization.
- How many times depend on the source language and the target machine
