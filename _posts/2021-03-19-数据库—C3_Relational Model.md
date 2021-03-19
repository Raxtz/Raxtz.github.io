---
layout:     post
title:      数据库—Chapter 3 Relational Model
subtitle:   数据库碎碎念
date:       2021-03-19
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 数据库
---

- The relational model was first introduced by Ted Codd of IBM Research in 1970
- and attracted due to its simplicity, elegance and mathematical foundations
- The model uses the concept of a mathematical relation – which looks like a table of values



## 3.1 Structure of Relational Databases

- **relation** --> table
  - denoted by $R(A_1, A_2, ..., A_n)$ where R is a **relation name** and $(A_1, A_2, ..., A_n)$ is the **relation schema** of R.
- **tuple** --> row
  - denoted by $A_i$
- **attribute** --> column
- **attribute value**
  - value stored in a table cell
- **relation instance**
  - same: contain the same set of tuples
- For each attribute of a relation, there is a set of permitted values, called the **domain** of that attribute.
  - denoted by $dom(A_i)$



## 3.2 Key

key / superkey, composite key, candidate key, primary key



A relation, say $r_1$, may include among its attributes <u>the primary key</u> of another relation, say $r_2$. This attribute is called a **foreign key** from $r_1$, referencing $r_2$.

The relation $r_1$ is also called the **referencing relation** of he foreign key dependency, and $r_2$ is called the **referenced relation** of the foreign key.

a **referential integrity constraint** requires that the values appearing in specified attributes of any tuple in the referencing relation also appear in specified attributes of at least one tuple in the referenced relation.



## 3.3 ER-to-Relational Mapping

- Typically, database designers begin with the ER model, which is very expressive and user-friendly to human
- Then, the ER model is mapped to the relational model for DBMS manipulations
- Database queries and updates will be written according to the relational model



- Translating Traditional ER Diagrams
- Translating Class Hierarchy



### Translating Traditional ER Diagrams

Steps:

1. Strong Entity Set
2. Weak Entity Set
3. 1-to-1 Relationship
4. 1-to-many Relationship
5. Many-to-many Relationship
6. Non-binary Relationship



#### Strong Entity Set

For each strong entity set E in the ER schema, 

- create a relation schema R that includes all the attributes of E. 
- choose one set of key attributes of E as a primary key for R.

Q: **Derived attribute**?
A: We have two choices.
Choice 1: Include this derived attribute
                Adv: We can directly obtain the value of the derived attribute
                Disadv: We may encounter some data inconsistencies
Choice 2: NOT include this derived attribute    (prefer)
                Adv: We can avoid data inconsistency
                Disadv: We need to perform some operations to obtain the value of the derived attribute

Q: **Composite attribute**?
A: We have two choices.
Choice 1: Include the high-level attribute only (e.g., address)
Choice 2: Include all low-level attributes (e.g., street, city, country)

一般选2吗？

Q: **Multi-valued attribute**?
A: We have two choices.
Choice 1: Include one attribute only (e.g., phone)
Choice 2: Create another table containing the primary key of the entity set and the multi-valued attribute

这里可以在phone的框里直接写多个电话吗？

不可以的话，选2减少重复元素比较好吗？



涉及到**binary relationship**，主要看**两个方面**：

1. 接近total程度（越接近total，越选为完整方——减少null）
2. degree的和（(degree的和 - 参与元素数)越少，越选为完整方——减少完整重复）
   （one的(degree的和 - 参与元素数)一般比many多）

一般来说，两个方面**都满足**时，才选为完整方，否则创个新表格。



#### Weak Entity Set

相当于one-to-many且many为total
（不同点为many是discriminator不是primary key，
只有一种方法，而且该方法完美满足两个条件）

For each weak entity set W in the ER model, 

- create a relation schema R, and include all attributes.
- In addition, include the primary key(s) of the owner(s). 
- he primary key of R is the combination of the primary key(s) of the owner(s) and the discriminator of the weak entity set W.



#### 1-to-1 Relationship

For each binary one-to-one (1:1) relationship set R

 T  ----  S

由于(degree和-参与元素数)都为0，不会重复；故只考虑谁最接近total，减少Null

choice 1: include the relationship into one schema (有一方接近total)

- 选最接近total的entity set为完整方S
- get primary key of T, and include it as foreign keys in S

- Include the attributes of the relationship set R as attributes of S.

choice 2: create a new relation (无一方接近total)

- Adv: 无Null
- Diadv：多了个relation
- 适用于Null较多，即两个都离total很远



#### 1-to-many Relationship

For each binary one-to-many relationship set 

 T  ----  S

一般来说：one方degree和多，为减少重复，完整方可选只有many

Choice 1: include the relationship into one schema (many方接近total)

- Include the primary key of entity set T as foreign key in relation schema of S.
- Include any attributes of the one-to-many relationship set as attributes of S.

Choice 2: create a new relation (many方不接近total)



#### Many-to-many Relationship

For each binary many-to-many relationship set



Choice 1: include the relationship into one schema (有一方degree和少且接近total)

- Include the primary key of T into the attribute of relation schema S.
- their combination will form the primary key of relation schema. 
- Also include attributes of the many-to-many relationship set as attributes of relation schema.

Choice 2: create a new relation (无一方degree和少且接近total)



#### Non-binary Relationship

创建新表格

For each non-binary relationship set R

- create a new relation schema S to represent R. 
- Include the primary keys of the participating entity sets as foreign key attributes in S. 
- Also include any attributes of the non-binary relationship set as attributes of S.

For non-binary relationships,

- The primary key of S is **usually** a combination of all the foreign keys that reference the relations representing the participating entity sets.  

- However if any entity set has a **key constraint** on the relationship (e.g., 1-to-many relationship), the primary key of the entity set can be used as a key for the relationship.



### Translating Class Hierarchy

Two methods:

1. 对superclass和每个subclass都创建relation, 而subclass的relation包含了superclass的primary key作为foreign key. （general method）
   - Adv: 可用于subclass不cover superclass的情况
   - Disadv: 多了一个表格；用两个表格才能明确relationship和superclass信息
2. 只对每个subclass创建relation，且每个relation包含了superclass完整的attribute.
   - Adv: 一个表格就能明确relationship和superclass信息
   - Disadv: 只适用于subclass cover superclass的情况；重复了superclass信息（subclass少点较适用）
