---
layout: post
title: 频率学派和贝叶斯学派
description: "介绍频率学派和贝叶斯学派的区别"
modified: 2016-04-13
tags: [draft]
categories: [MachineLearning]
---
![](http://imgs.xkcd.com/comics/frequentists_vs_bayesians.png)

> 问：如果笑话里的人不是金色头发，那么这个笑话的好笑程度是增加、不变、还是减少？  
> 频率学派学者：减少。
> 贝叶斯学派学者：不变。 
> 金色头发的贝叶斯学派学者：增加。


> 贝叶斯学派就是心里期望着马，但是却瞥见了驴，并强烈认为自己看到的是骡子的人。
> 贝叶斯学派就是为了给出你猜想结果的而在诊断结果出来前询问你想法的人。

抛起一枚硬币，硬币落下后正面朝上的概率为$P$，反面朝上的概率为$1-P$。
一枚硬币抛$n$次，其中正面朝上$x$次。

对于频率学派来说，$P$是一个确定的量，抛硬币的过程可以反复一直执行，对于现在这种情况，他得出的结论是，对于$1-\alpha$的置信度，$P$位于$[P_l, P_u]$之间。其中$P_l,P_u$满足：

$$
\begin{equation}
\sum_{k=0}^{x-1}C_n^k P_l^k (1 - P_l)^{n-k}=\frac{\alpha}{2}
\label{p_l}
\end{equation}
$$
$$
\begin{equation}
\sum_{k=x+1}^{n}C_n^kP_u^k(1-P_u)^{n-k}=1-\frac{\alpha}{2}
\label{p_u}
\end{equation}
$$