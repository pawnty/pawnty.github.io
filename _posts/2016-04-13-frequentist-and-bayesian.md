---
layout: post
title: 频率学派和贝叶斯学派
description: "介绍频率学派和贝叶斯学派的区别"
modified: 2016-04-13
tags: [draft]
categories: [MachineLearning]
---
# 频率学派与贝叶斯学派

![xkcd](http://imgs.xkcd.com/comics/frequentists_vs_bayesians.png)

> 一台可以探测太阳是否爆炸且很少说谎的机器报告太阳已经爆炸。
> 频率学派：“我认为太阳爆炸了。”
> 贝叶斯学派：“赌你50它没炸。” 
> ——[xkcd](http://xkcd.com/1132/)

频率学派认为数据由采样得来，并且实验是可重复的，但是参数是一直固定的。而贝叶斯学派则认为数据是固定的，参数是不确定的，并且可以根据数据不断更新参数的不确定性。

对于含有隐含变量的结构较复杂的模型，贝叶斯学派更加简单。并且，贝叶斯学派能够将已有的知识和经验融入到模型中，从而得到更好的结果。
但是在1950-1990年间，几乎没有人做贝叶斯分析。原因在于贝叶斯学派的分析需要大量的计算，而计算机不仅非常慢，而且没有普及。随着计算机科学的发展，以及新的推断方式的提出，尤其是马尔科夫链蒙特卡洛方法的提出，贝叶斯学派得到大量的应用，更多实际问题和复杂的模型得以解决。

贝叶斯建模一般过程是先为未知的参数选择先验概率分布$p(\theta)$，然后根据贝叶斯公式得到的后验概率
$$\begin{equation}
p(\theta\vert x)=\frac{p(\theta)p(x\vert \theta)}{\int p(\theta)p(x\vert \theta) d\theta}\label{bayes}
\end{equation}
$$
更新参数的分布。在实际问题中， $\eqref{bayes}$式往往写不出公式。比较常见的情况是模型除了可观测变量之外，还包含隐含变量，使得用贝叶斯公式求参数的后验分布时涉及到对隐含变量的积分，
$$
\begin{equation}
p(\theta\vert X)=\frac{p(\theta)\int_Zp(X, Z\vert \theta)dZ}{\int p(\theta)p(X, Z\vert \theta) dZd\theta}
\end{equation}
$$
隐含变量可能维度非常高，从而使得后验概率无法写出表达式。

对于贝叶斯学派，参数的先验概率分布的选择非常重要。先验可以是研究者的直觉、领域专家的知识和经验以及相关的其他方法和数据。贝叶斯学派比较受诟病的一点是，其先验的选取在很大程度上是为了计算上的方便。最常用的一种先验是共轭先验分布。使用共轭先验分布计算出的后验分布会和先验分布保持同一种形式，只是参数不同。例如，多项式分布的共轭先验分布是Beta分布，当使用Beta分布作为先验时，得到的后验分布也是Beta分布。以下是一些调侃贝叶斯学派先验分布选择的主观性的笑话。

> 有一个主人公是美国人的笑话。
> 问：如果笑话里的人不是美国人，那么这个笑话的好笑程度是增加、不变、还是减少？  
> 频率学派的学者：减少。
> 贝叶斯学派的学者：不变。 
> 贝叶斯学派的美国学者：增加。

> 贝叶斯学派就是心里期望着马，但是却瞥见了驴，并强烈认为自己看到的是骡子的人。

> 贝叶斯学派就是为了给出你猜想结果的而在诊断结果出来前询问你想法的人。

抛起一枚硬币，硬币落下后正面朝上的概率为$P$，反面朝上的概率为$1-P$。
一枚硬币抛$n$次，其中正面朝上$x$次。

对于频率学派来说，$P$是一个确定的量，抛硬币的过程可以反复一直执行，对于现在这种情况，他得出的结论是，对于$1-\alpha$的置信度，$P$位于$[P_l, P_u]$之间。其中$P_l,P_u$满足：

$$
\begin{equation}
\sum_{k=0}^{x-1}C_n^k P_l^k (1 - P_l)^{n-k}=\frac{\alpha}{2}\label{p_l}
\end{equation}
$$

$$
\begin{equation}
\sum_{k=x+1}^{n}C_n^kP_u^k(1-P_u)^{n-k}=1-\frac{\alpha}{2}\label{p_u}
\end{equation}
$$

而贝叶斯学派会先给出一个P的先验分布，
$$\begin{equation}
\theta \sim \mathrm{Beta}(a, b)
\end{equation}$$

$$\begin{equation}
p(\theta)=\mathrm{Beta}(\theta\vert a, b)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}\theta^{a-1}(1-\theta)^{b-1}
\end{equation}$$
$$\begin{equation}
\Gamma(t)=\int_0^\infty x^{t-1}e^{-x}dx
\end{equation}$$

$$
\begin{equation}
p(\theta\vert x)=\frac{p(\theta)p(x|\theta)}{\int p(\theta)p(x|\theta) d\theta}
= Beta(\theta\vert a + x, a + n - x)
\end{equation}
$$