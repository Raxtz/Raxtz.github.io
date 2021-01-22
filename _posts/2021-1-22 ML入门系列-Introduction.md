---
layout:     post
title:      ML入门系列-Introduction
subtitle:   李宏毅2020机器学习碎碎念
date:       2021-1-22
author:     lora
header-img: img/the-first.png
catalog:   true
tags:
    - 机器学习
---

>**“机器学习就是自动找函式。”**

## 1. 你想找什么样的函式？
【不同函式，对应不同机器学习任务】

看输出：
- 输出scalar（数值）<br> —— **Regression**
- 输出只有两个可能(e.g, Yes or No)<br> —— **Binary Classification** ｛RNN｝
- 输出是在固定的一个集合（元素数量大于2）中的一个元素<br> —— **Multi-class Classification** ｛CNN｝
- 生成有结构的复杂东西（e.g,句子，图片）<br> —— **Generation**｛Seq2seq, GAN｝
*Classification包含Binary Classification与Multi-class Classification*

简单概括为：
- **Regression**: 生成一个数值
- **Classification**: 做选择题
- **Generation**: 创造。 

## 2. 怎么告诉机器，你想找什么样的函式？
- **Supervised Learning** {Regression, Classification, RNN, CNN, Seq2seq}<br>使用labeled data（带标注的训练数据，即训练数据知道每个输入数据对应的正确输出）。让机器自动找出Loss最低的一个函式。

- **Reinforcement Learning** {Reinforcement Learning}<br>用Reward来引导机器学习的方向。

- **Unsupervised Learning** {Unsupervised Learning(Auto-encoder), GAN}<br>使用unlabeled data。

## 3. 机器怎么找出你想要的函式？
1. 给定函式的寻找范围
- **Linear** ｛Regression, Classification｝
- **Network Architecture** ｛RNN, CNN｝
	* {RNN} ——> {Seq2seq}
    * {CNN} ——> {GAN}, {Unsupervised Learning(Auto-encoder), Anomaly Detection, Transfer Learning(Domain Adversarial Learning), Meta Learning}, {Explainable AI, Adversarial Attack, Network Compression}
2. 函式寻找方法（**Learning Algorithm**）
- Gradient Descent
	* Implement the algorithm by yourself
    * Deep Learning Framework
    
## 4. 前沿研究
- **Explainable AI** <br> 给出输出这样结果的理由。
- **Adversarial Attack** <br> 针对机器输出的攻击
- **Network Compression** <br> 把庞大的modal缩小
- **Anomaly Detection**<br> 机器知道自己并不知道 输入的东西应该给的输出是什么。
- **Transfer Learning**(Domain Adversarial Learning)<br> 测试资料与训练资料的distribution不同，其导致的正确率下降的补救方法。
- **Meta Learning** = Learn to learn. 学习如何学习。<br>
	* 机器学习：写一个程序，让机器拥有学习能力。（学习方法由人设计）
    * 元学习：写一个程序，让机器拥有如何学习的能力，再使用该能力，让机器掌握学习能力。（学习方法由机器设计）
- **Life-long Learning** 终身学习 (Continuous Learning, Never Ending Learning, Incremental Learning)<br> 让机器一步步地掌握多种技能。
{{Explainable AI, Adversarial Attack, Network Compression} 基于 {CNN} 的结果。} 
