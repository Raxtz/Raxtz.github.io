---
layout:     post
title:      数据库—Chapter 4 Relational Algebra
subtitle:   数据库碎碎念
date:       2021-03-19
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 数据库
---

The **relational query languages** (a **query language** associated with the **relational model**) define a set of operations that operate on tables, and output tables as their results. These operations can be combined to get expressions that express desired queries.

**Relational algebra** is a **relational query language**.

The **relational algebra** provides a set of operations that take one or more relations as input and return a relation as an output. Practical query languages such as SQL are based on the relational algebra, but add a number of useful syntactic features.

- Relational algebra includes the **queries in terms of operators**
- Every **operator** in relational algebra takes one or two relations as parameters and return a relation. 



The relational algebra is a *procedural* query language.

Fundamental Operations:

- Project
- Select
- Union
- Set difference
- Cartesian product
- Rename

Project, Select, Rename: unary
Union, Set difference, Cartesian product: binary

Operations defined in terms of the fundamental operations:

- Set Intersection
- Join (Natural join, Condition-Join, Outer Join)
- Assignment (ppt无)
- Division

Each operation returns a relation, and operations can be *composed*.

In general, since the result of a relational-algebra operation is of the same type (relation) as its inputs, relational-algebra operations can be composed together into a **relational-algebra expression**.



Since a relation is a set, **any duplicate rows are eliminated** in the **relational algebra**.



### 4.1.1 The Project Operation

unary

Projection is denoted by the uppercase Greek letter pi ($\Pi$). We list those attributes that we wish to appear in the result as a subscript to $\Pi$. The argument relation follows in parentheses. 

$\Pi_L(R)$

- Delete/remove attributes that are not in projection list L.
- Schema of result contains exactly the **fields** in the projection list, with the same names that they had in the input relation.

- eliminates duplicates



## 4.1.2 The Select Operation

unary

The select operation selects **tuples** that satisfy a given predicate. 

We use the lowercase Greek letter sigma ($\sigma$) to denote selection. The predicate appears as a subscript to $\sigma$. The argument relation is in parentheses after the $\sigma$.

$\sigma_c(R)$

In general, we allow comparisons using $=, \not=, <, \leq, >,$ and $\geq$ in the selection predicate. Furthermore, we can combine several predicates into a larger predicate by using the connectives $and (\wedge), or(\vee),$ and $not(\neg)$. 



## 4.1.3 The Union Operation

binary

set operation

$r \cup s$

Input: two relations, Output: one relation.

In general, we must ensure that unions are taken between **compatible** relations. For a union operation $r \cup s$ to be valid, we require that two conditions hold:

1. The relations $r$ and $s$ must be of the same arity. That is, they must have the **same number of attributes**.
2. The **domains** of the $i$th attribute of $r$ and the $i$th attribute of $s$ must be the same, for all $i$.



## 4.1.4 The Set-Difference Operation

binary

set operation

The set-difference operation, denoted by $-$, allows us to find tuples that are in one relation but are not in another. 

$r - s$

Input: two relations, Output: one relation



## 4.1.5 The Cartesian-Product Operation

binary

The Cartesian-product operation, denoted by a cross ($\times$), allows us to combine information from any two relations. 

$r_1 \times r_2$

Combines each row of one table with every row of another table.

This naming convention requires that the relations that are the arguments of the Cartesian-product operation have distinct names.



## 4.1.6 The Rename Operation

The rename operator, denoted by the lowercase Greek letter rho ($\rho$).

book:

$\rho_x(E)$

$\rho_{x(A_1, A_2, ..., A_n)}(E)$

ppt:

$\rho(R'(N_1->N'_1, ..., N_k->N'_k), R)$



## 4.2.1 The Set-Intersection Operation

binary

set operation

$r \cap s = r - (r - s)$



## 4.2.2 The Natural-Join Operation and the Condition-Join Operation

binary

The natural-join operation 

- forms a Cartesian product of its two arguments,
- performs a selection forcing equality on those attributes that appear in both relation schemas,
- and finally removes duplicate attributes.

Consider two relations $r(R)$ and $s(S)$. The natural join of $r$ and $s$, denoted by $r \Join s$, is a relation on schema $R \cup S$ formally defined as follows:

$r \Join s = \Pi_{R \cup S}(\sigma_{r.A_1 = s.A1 \wedge r.A_2 = s.A_2 \wedge ... \wedge r.A_n = s.A_n}(r \times s)) $

$= \sigma_{r.A_1 = s.A1 \wedge r.A_2 = s.A_2 \wedge ... \wedge r.A_n = s.A_n}(r \times s)$

where $R \cap S = {A_1, A_2, ..., A_n}$

if  $R \cap S = \empty$, $r \Join s = r \times r$.

associative:

$(r \Join s) \Join t = r \Join (s \Join t)$



The **theta join** / **condition-join** operation is a variant of the natural-join operation that allows us to combine a selection and a Cartesian product into a single operation.

Let $\theta$ be a predicate on attributes in the schema $R \cup S$.

$r \Join_\theta s = \sigma_\theta(r \times s)$



## 4.2.3 The Assignment Operation

The assignment operation is denoted by $\leftarrow$.

The evaluation of an assignment does not result in any relation being displayed to the user. Rather, the result of the expression to the right of the $\leftarrow$ is assigned to the relation variable on the left of the $\leftarrow$. This relation variable may be used in subsequent expressions.



## 4.2.4 Outer Join Operations

The outer-join operation is an extension of the join operation to deal with missing information.

The outer join operation works in a manner similar to the natural join operation we have already studied, but preserves those tuples that would be lost in an join by creating tuples in the result containing null values.

- left outer join 
- right outer join
- full outer join



## 4.2.5 The Division Operation

The division operator of relational algebra, "$\div$" (book).

Let $r(R)$ and $s(S)$ be relations, and let $S \subseteq R$; that is, every attribute of schema $S$ is also in schema $R$. Then $r \div s$ is a relation on schema $R - S$ (that is, on the schema containing all attributes of schema $R$ that are not in schema $S$). A tuple $t$ is in $r \div s$ if and only if both of two conditions hold:

- $t$ is in $\Pi_{R-S}(r)$
- For **every tuple $t_s$** in $s$, there is a tuple $t_r$ in $r$ satisfying both of the following:
  - $t_r[S] = t_s[S]$
  - $t_r[R-S] = t$

ppt:

$r / s$

