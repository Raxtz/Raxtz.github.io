---
layout:     post
title:      ML入门系列-Regression
subtitle:   李宏毅2020机器学习碎碎念
date:       2021-03-03
author:     小熊pink
header-img: img/the-first.png
catalog:   true
tags:
    - 机器学习
---

## 1. Step 1: Model (选择函数集合)

> 1. 找函数
> 2. 定参数

找function set (model) ($f_1, f_2, f_3,...$)

这里先找个简单的: $y = b + w*x_{cp}$

$w$ and $b$ are parameters (can be any value)
不同的$w$,$b$定义了不同的$f$

Linear Model: $y = b + \sum w_ix_i$

+ $x_i$: feature
+ $w_i$: weight
+ $b$: bias



## 2. Step 2: Goodness of Function (敲定Loss Function)

>  定参数，需要参考给定的loss function，选出使Loss function结果最小的参数即可。
>
>  （loss function + 解法 -->参数解的结果）

1)这里用Supervised Learning，使用labeled training data (收集$x^i$与$\hat{y}^i$，使用$x_{cp}^i$与$\hat{y}^i$)实际收集了10组。

2)定义一个function的好坏，即定义Loss Function L

$L(f) = L(w,b) = \sum_{n=1}^{10}(\hat{y}^n - (b+wx_{cp}^{n}))^2$



## 3. Step 3: Best Function (解法)

**1.**

$f^* = \mathop{\arg\min_{f}}L(f)$

$w^*,b^* = \mathop{\arg\min_{w,b}}L(w,b) = \mathop{\arg\min_{w,b}}\sum_{n=1}^{10}(\hat{y}^n - (b+wx_{cp}^{n}))^2$

解法：

+ 线代
+ Gradient Descent (L可微分)



**2.Gradient Descent**

2.1 Example 1

Consider loss function L(w) with one parameter w: $w^* = \mathop{\arg\min_{w}}L(w)$

+ (Randomly)Pick an initial value $w^0$.
+ Compute $\frac{dL}{dw}|_{w=w^0}$
+ $w^1 \leftarrow w^0 - \eta\frac{dL}{dw}|_{w=w^0}$ //意思：$\frac{dL}{dw}|_{w=w^0}$大，移动大；$\eta$大，移动大。

**$\eta$: learning rate**

+ 迭代下去，直到$\frac{dL}{dw}|_{w=w^i}$为0。
  2.2 缺点
  可能会只找到local optimal而不是global optimal（与Loss function, initial value等有关）。

2.3 Example 2

How about two parameters? $w^*,b^* = \mathop{\arg\min_{w,b}}L(w,b)$

+ (Randomly)Pick an initial value $w^0$, $b^0$.
+ Compute $\frac{dL}{dw}|_{w=w^0,b=b^0}$, $\frac{dL}{db}|_{w=w^0,b=b^0}$
+ $w^1 \leftarrow w^0 - \eta\frac{dL}{dw}|_{w=w^0,b=b^0}$, $b^1 \leftarrow b^0 - \eta\frac{dL}{db}|_{w=w^0,b=b^0}$

2.4 Gradient Descent of Linear Regression

在Linear Regression中，如果定义的Loss Function为之前的类型，则该Loss Function为convex，没有local optimal，只有global optimal，故使用Gradient Descent一定可求解正确。

> Linear Regression + 误差平方和的Loss Function --解出参数--> 一定为global optimal



## 4. How's the results? (衡量具体函数好坏)

> 用generalization衡量具体函数的好坏。

看看Average error in training data，而真正关心的是Generalization的情况，即the error on new data (testing data)。Average error in testing data 通常会比Average error in training data大。



## 5. How can we do better? (函数的改进)

1. 考虑更复杂的model（增加次数）。[model层面] $\rightarrow 6$ 
2. 考虑其他影响因素。[model层面] $\rightarrow 7$ 
3. Regularization[Loss Function层面] $\rightarrow 7.5$ 



## 6. Model Selection 结果分析

| 次数(↑) | training(↓) | testing(↓↑) |
| :-----: | :---------: | :---------: |
|    1    |    31.9     |    35.0     |
|    2    |    15.4     |    18.4     |
|    3    |    15.3     |    18.1     |
|    4    |    14.9     |    28.2     |
|    5    |    12.8     |    232.1    |

**Overfitting**: a more complex model does not always lead to better performance on testing data.

We should select a suitable model.

## 7. Consider hidden factors

1. Let's collect more data

2. What are the hidden factors? 

3. Consider $x_{s}$.		<br>3.1 Back to step 1: Redesign the Model			<br>If $x_{s} = $ Pidgey: $y = b_1 + w_1*x_{cp}$<br>If $x_{s} = $ Weedle: $y = b_2 + w_2*x_{cp}$<br>If $x_{s} = $ Caterpie: $y = b_3 + w_3*x_{cp}$<br>If $x_{s} = $ Eevee: $y = b_4 + w_4*x_{cp}$			<br>The model above is also a linear model:<br>$y = b_1\cdot\delta(x_{s} = Pidgey) + w_1\cdot\delta(x_{s} = Pidgey)x_{cp}\\ + \ b_2\cdot\delta(x_{s} = Weedle) + w_2\cdot\delta(x_{s} = Weedle)x_{cp}\\ + \ b_3\cdot\delta(x_{s} = Caterpie) + w_3\cdot\delta(x_{s} = Caterpie)x_{cp}\\ + \ b_4\cdot\delta(x_{s} = Eevee) + w_4\cdot\delta(x_{s} = Eevee)x_{cp}$    <br>$\delta(条件)$ 中，若条件正确，则输出1；反之，输出0。

   3.2 Result

| Trainig | Testing |
| :-----: | :-----: |
|   3.8   |  14.3   |

4. Consider $x_{w}$(weight), $x_{h}$(height), and $x_{hp}$
   4.1 //具体公式省略
   4.2 Result

| Trainig | Testing |
| :-----: | :-----: |
|   1.9   |  102.3  |

​		Overfitting !!

5. Back to step 2: Regularization

   5.1

   Model: $y = b+\sum_{i}{w_ix_{i}}$

   Loss Function: $L = \sum_{n}(\hat{y}^n - (b+\sum_{i}{w_ix_{i}^{n}}))^2 + \lambda\sum_{i}(w_i)^2$

   $\lambda$ 越大，选出的model越光滑。

Q: Why smooth functions are preferred?
   A: If some noises corrupt input $x_i$ when testing, a smoother function has less influence. （去除x的波动噪声）

   Q: 怎么写Loss Function中Regularization部分的式子？

   A: 给每个$x_i$加上$\Delta x$，想让$\Delta y$尽可能小，故应让$\Delta y$中所有$\Delta x$的系数都变小，则可让系数的平方和纳入Loss Function。

   5.2 Result

| $\lambda$(↑) | Training(↑) | Testing(↓↑) |
| :----------: | :---------: | :---------: |
|      0       |     1.9     |    102.3    |
|      1       |     2.3     |    68.7     |
|      10      |     3.5     |    25.7     |
|     100      |     4.1     |    11.1     |
|     1000     |     5.6     |    12.8     |
|    10000     |     6.3     |    18.7     |
|    100000    |     8.5     |    26.8     |

   越平滑就越不拟合training data，但是因为可去除x的波动噪声，对testing data可能较拟合。
