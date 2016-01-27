---
layout: post
disqus_comments: yes
title: "Principal Component Analysis"
---
In practice, high-dimensinal data usually can be embedding in a much lower 
dimensional manifold. We can use *principal component analysis(PCA)* to transform
to data to a linear lower dimensional manifold to get rid of *the curse 
of dimensionality*. PCA is widely used in industry and has various applications
such as dimensinal reducing, data visualization and lossy compressing.

There are two ways to derive PCA, each from a different view, which will 
be discussed in the next two section.

## Aproxximation View
As the data often lies in a low dimensional manifold, we try to use a low dimensional
data to aproxximate the original data.
Suppose we have a original dataset $$\{x_n \in \mathrm R^D\}, n = 1, 2, \dots, N$$, 
we want to choose a set of basis, $$\{u_i \in \mathrm R^D \}, i = 1, 2, \dots, D$$, which
satisfies 

$$
u_i^{\mathrm T} u_i = 1,\\
u_i^{\mathrm T} u_j = 0, i \neq j.
$$

We use a $$M$$ dimensional data $$a_n$$ to represent a original data $$x_n$$, 
where $$M < D$$. The proximation is defined by

$$
\hat x_n = \sum_{i=1}^M a_{ni}u_i + \sum_{i=M+1}^D b_i u_i.
$$
where $$b_i$$ does not depend on specific data. To see what is $$a_n$$, we multiply
each side by $$u_i$$ and use the properties of the basis, we can find that 
$$a_i = u_i^{\mathrm T}x_n$$, wich can be determined by the basis.

To find the proper basis, we minimize the loss function

$$
J = \frac{1}{N}\sum_{n=1}^{N}||\hat x_n - x_n||_2^2
  = \frac{1}{N}\sum_{n=1}^{N}||\sum_{i=M+1}^D (b_i - u_i^{\mathrm T}u_i)u_i||_2^2
$$

according to $$b_i$$ and $$u_i$$, repectively. We first set the dirivetive according
to $$b_i$$ to $$0$$ and get $$b_i = (u_i^{\mathrm T} \bar x)u_i$$, where $$\bar x = \frac{1
}{N}\sum_{n=1}^N x_n$$. Substitude $$b_i$$ back to $$J$$, we get

$$
J = \sum_{i=M+1}^D u_i^{\mathrm T}S u_i
$$

where we have define $$S=\frac{1}{N}\sum_{n=1}^N (x_n - \bar x)(x_n - \bar x)^{\mathrm T}$$,
which is empirical covariance of the dataset.
To solve minimize $$J$$ directly is not easy, but we can show that if $$u_i$$ is a eigenvector
of $$S$$ and $$\lambda_i$$ is its corresponding eigenvalue, which means

$$
S u_i = \lambda_i u_i, \\
u_i^{\mathrm T} S u_i = \lambda_i,
$$

then $$J = \sum_{i=M+1}^D \lambda_i$$. Thus we can choose $$u_i, i=M+1, \dots, D$$ to be eigen
vectors whose eigenvalue are top $$D-M+1$$ smallest. To put it in another word, we should
choose eigenvectors with top $$M$$ largest eigenvalue to approximate the original data.

## Maxmizing-Information View
