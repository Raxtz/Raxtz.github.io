---
layout:     post
title:      数据库—Chapter 1 Introduction
subtitle:   数据库碎碎念
date:       2021-03-13
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 数据库
---
# Chapter 1 Introduction

A **database-management system (DBMS)**

- a collection of interrelated data and a set of programs to access those data.
- a collection of software programs to enable users to create, maintain and utilize a database.
- 操作：增删改查

**database**: a collection of data, typically describing the activities of one or more related organizations

- A database can be of any size and of varying complexity.

The primary goal of a DBMS is to provide a way to store and retrieve database information that is both *convenient* and *efficient*.



## 1.2 Purpose of Database System

Before DBMSs were introduced, organizations usually stored information in **file-processing systems**. 

Disadvantages: （in the file-processing system）

- Data redundancy and inconsistency（重复出现）
- Difficulty in accessing data / Data isolation
- Integrity problems（consistency constraints）
- Atomicity problems（转账增减同步）
- Concurrent-access anomalies（同步）
- Security problems（权限）



## 1.3 View of Data

### 1.3.1 Data Abstraction

- **Physical level.**
  describes **how** the data are actually stored
  describes complex low-level data structures in detail
- **Logical level (Conceptual level).** 
  describes **what** data are stored in the database, and what relationships exist among those data
  describes the entire database in terms of a small number of relatively simple structures
  **physical data independence**
- **View level.**
  describes only part of the entire database
  simplify users' interaction with the system
  The system may provide many views for the same database.



### 1.3.2 Instances and Schemas

**schema**: the overall design of the database（changed infrequently）

- the definition of a database. It defines the meaning of data.

**instance**: the collection of information stored in the database at a particular moment（changed frequently）



Database systems have several schemas, partitioned according to the levels of abstraction.

**physical schema**: describes the database design at the physical level

**logical schema**: describes the database design at the logical level

**subschemas**(several schemas at the view level): describe different views of the database



### 1.3.3 Data Models

**Data Model**: 

- a collection of conceptual tools for describing data, data relationships, data semantics, and consistency constraints
- underlying the structure of a database
- provides a way to describe the design of a database at the physical, logical, and view levels



A description of data in terms of a data model is called a **schema**. （我认为data model是schema的一部分）



**Categories**

- **Object-Based Logical Models**
  - **Entity-Relationship Model (E-R Model)**
    - uses a collection of basic objects, called *entities*, and *relationships* among these objects.
    - widely used in database design
- **Record-Based Logical Models**
  the database is structured in fixed-format records of several types
  - **Relational Model**
    - uses a collection of tables to represent both data and the relationships among those data
    - Tables are also known as **relations**.
    - Each table contains records of a particular type. Each record type defines a fixed number of **fields**, or **attributes** (columns). 
    - the most widely used data model



Four different categories:

- **Relational Model**
- **Entity-Relationship Model (E-R Model)**
  - uses a collection of basic objects, called *entities*, and *relationships* among these objects.
  - widely used in database design
- **Object-Based Data Model**
  - **Object-Oriented Data Model**
    - can be seen as extending the E-R model with notions of encapsulation, methods (functions), and object identity.
  - **Object-Relational Data Model** （不知道属不属于object-based）
    - combines features of the object-oriented data model and relational data model
- **Semistructured Data Model**
  - permits the specification of data where individual data items of the same type may have different sets of attributes
  - The **Extensible Markup Language (XML)** is widely used to represent semistructured data.

Historically, the **network data model** and the **hierarchical data model** preceded the relational data model. These models were tied closely to the underlying implementation, and complicated the task of modeling data. As a result they are used little now, except in old database code that is still in service in some places.



## 1.4 Database Languages

A database system provides a **data-definition language** to specify the database schema and a **data-manipulation language** to express database queries and updates.

In practice, the data-definition and data-manipulation languages are not two separate languages; instead they simply form parts of a single database language, such as the widely used SQL language.

### 1.4.1 Data-Manipulation Language

A **data-manipulation language (DML)** is a language that enables users to access or manipulate data as organized by the appropriate data model

The types of access are: (增删改查)

- Retrieval of information stored in the database
- Insertion of new information into the database
- Deletion of information from the database
- Modification of information stored in the database

There are basically two types:

- **Procedural DMLs** require a user to specify *what* data are needed and *how* to get those data.
- **Declarative DMLs** (**nonprocedural DMLs**) require a user to specify *what* data are needed *without* specifying how to get those data.

A **query** is a statement requesting the retrieval of information.
The portion of a DML that involves information retrieval is called a **query language**.
Although technically incorrect, it is common practice to use the terms *query language* and *data-manipulation language* synonymously.

e.g. SQL

The levels of abstraction apply not only to defining or structuring data, but also to manipulating data.



### 1.4.2 Data-Definition Language

a **data-definition language (DDL)**

- express a set of definitions to specify a database schema
- specify additional properties of the data

a **data storage and definition** language (a special type of DDL)

- express a set of statements to specify the storage structure and access methods used by the database system
- these statements define the implementation details of the database schemas, which are usually hidden from the users

Database systems implement consistency constraints constraints (integrity constraints) that can be tested with minimal overhead:

- Domain Constraints.
- Referential Integrity.
- Assertions.
  An assertion is any condition that database must always satisfy.
  Domain constraints and referential-integrity constraints are special forms of assertions. 这里指除上两个外的其他限制条件
- Authorization. 权限（增删改查）
  read authorization
  insert authorization
  update authorization
  delete authorization

The output of the DDL is placed in the **data dictionary**, which contains **metadata** -- that is, data about data.
The data dictionary is considered to be a special type of table that can only be accessed and updated by the database system itself (not a regular user).
The database system consults the data dictionary before reading or modifying actual data.

