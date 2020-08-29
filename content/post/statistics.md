---
title: "Statistics"
date: 2020-04-28T17:13:47+08:00
lastmod: 2020-04-28T17:13:47+08:00
draft: true
tags: []
categories: []

reward: false
mathjax: true
mathjaxEnableSingleDollar: true
mathjaxEnableAutoNumber: false
---

很早就想要学习一下概率与统计学的知识了. 现在开始吧.

<!--more-->
---
## 概率

### 条件概率
$ P(A|B) = \frac{P(A\cap B)}{P(B)} $, 在B前提下A的概率=(A和B交集的概率)/B概率  
理解: 把右边P(B)移到左边,即B发生的概率乘以条件概率,等于交集概率.  

### 随机变量
随机变量 X 是一个样本空间与实数域上的映射。例如：样本空间{男，女} <=> {0,1}, 
因为我们通常只关心 X(s) = 0 的概率，所以用随机变量可以将样本空间转成我们熟悉的实值函数。
X(s) 可以看成是样本 s 在实数轴上的坐标(以防s是与实数无关的样本)。此时分布函数 F(x) 就是
坐标 X(s) 落在 $ (-\infty, x] $ 之间的概率。

$ X ~ U(a,b) $ : 随机变量X在[a,b]区间符从均匀分布(Uniform Distribution)
$ X ~ N(\mu,\sigma^2) $ : 随机变量X符从正态分布(Normal Distribution)
$ EXP(\theta) $: 指数分布
$ P(\lambda) $: 泊松分布

## 期望

## 统计