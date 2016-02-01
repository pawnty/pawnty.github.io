---
layout: post
title: KL散度及其在统计推断中的应用
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

在统计模型中有两种变量：随机变量和模型参数。随机变量随着数据的增多而增多，其中包含可以观测到的可见随机变量和观测不到的隐含随机变量，分别表示为$X$和$W$。模型参数不随数据的增多而增多，是控制模型假定存在的量，用$\theta$来表示。

有一种确定$\theta$的方法是选择使得可见变量的似然最大的值作为模型的参数，即

$$
\theta^* = \arg\max_\theta p(X;\theta).
$$

其中$p(X;\theta) = \int p(X,W;\theta)dW$.至此，推断问题已经被转化为一个优化问题，我们可以采用一般的优化方法来解决。常用的方法有：
	1. 求导并另其等于$0$，直接解出$\theta$;
	2. 	 梯度下降法，求出导数表达式，逐步迭代
第一种方法要求$\theta$可以直接表达为一个解析式，第二种方法要求给定一个$\theta$值，可以表示出在这点上的导数。但是，有些问题中这两点都无法满足。在这些问题里，有一些是由于有隐含变量未知导致的，加入隐含变量问题会变得简单。这样的问题可以用EM算法求解。

由概率的性质可知
$$
\ln p(X;\theta) = \ln p(X,W;\theta) - \ln p(W\vert X;\theta)
$$

两边对一个关于$W$的分布求积分并整理可得
$$
\ln p(X;\theta) = \int \ln\frac{ p(X,W;\theta)}{q(W)} q(W)dW - \int \ln \frac{p(W\vert X;\theta)}{q(W)} q(W)dW.
$$
注意到等式右边第二项是$q(\cdot)$到$p(\cdot\vert X;\theta)$的KL散度$D(q(\cdot)\vert\vert p(\cdot\vert X;\theta))$。由于KL散度非负，所以右边第一项是似然的下界，称之为*ELBO*(evidence lower bound)。

假设ELBO项可以通过优化$\theta$增大，并且对于给定的$\theta$，我们可以求得$p(W\vert X;\theta)$，那么我们就可以采用EM算法来求最大似然的解。

EM算法的步骤：
1. 随机初始化$\theta$
2. 迭代以下两个步骤直至收敛
	+ E步骤：使得$q(W)=p(W\vert X;\theta)$;
	+ M步骤：优化ELBO项，更新$\theta$.

注意，在E步骤，由于变化的只是$q$，因此似然并没有变化，又由KL散度的性质可知，此时KL项为0，进而ELBO项变大。在M步骤，优化$\theta$使得ELBO项变大，由于$\theta$变化，故旧的$p$已经不再是$p(W\vert X;\theta)$，因此KL项也变大。而似然是ELBO项和KL项的和，故似然也变大。可见，在达到最优解之前，每一次迭代都会使似然变大。当达到最优解时，$\theta$不再变化，KL项为$0$，ELBO项也达到最优解。