---
layout: post
title: KL散度及其在统计学习中的应用
description: "介绍KL散度的定义和性质，以及EM算法、变分推断和"
modified: 2016-01-29
tags: [draft]
categories: [MachineLearning]
---
##介绍

KL散度（Kullback Leibler Divergence）又称相对熵（Relative Entropy），在信息论中用于表示采用概率$p$的最优编码来传输真实概率为$q$的数据所需要的额外信息量。它的定义式为

$$D(p\|q)=-\int p(x)\ln\frac{q(x)}{p(x)}dx.$$

由于熵（entropy）是传输$p$所需要的最小信息量，可知$D(p \vert\vert q)\ge 0$。这一点也可由杰森不等式得到：

$$-\int p(x)\ln\frac{q(x)}{p(x)}dx\ge-\ln(\int p(x)\frac{q(x)}{p(x)}dx)=-\ln 1=0.$$

在这里$-\ln(\cdot)$是凸函数。
## EM算法

在统计模型中有两种变量：随机变量和模型参数。随机变量随着数据的增多而增多，其中包含可以观测到的可见随机变量和观测不到的隐含随机变量，分别表示为$X$和$$W$$。模型参数不随数据的增多而增多，是控制模型假定存在的量，用$$\theta$$来表示。

有一种确定$$\theta$$的方法是选择使得可见变量的似然最大的值作为模型的参数，即

$$
\theta = \arg\max_\theta P(X).
$$

其中$$P(X) = \int P(X,W)dW$$.