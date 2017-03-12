---
layout: post
title: "numerical integration"
disqus_comments: yes
---
## numerical approximation for integration
When solving integration problem $$I = \int_a^b f(x) dx$$, 
the *Fundamental theorem of Calculus*  will not work if there is not a closed-
form expression for the result.  We resort to numerical method the
compute the approximate result. To achieve this goal, 
we devide $$[a, b]$$ to $$n$$ equal-width intervals. 
The width of the intervals is denoted by $$h=\frac{b-a}{n}$$. 
For each interval $$[a_{i-1}, a_i]$$, 
where $$a_i = a + i h, \quad i = 0, 1, \dots, n$$, 
its middle point is denoted by $$x_i$$, 
we use a simpler function $$s(x)$$ to approximate the original $$f(x)$$. 
The approximate result could be expressed by
$$
I_n = \sum_{i=1}^n\int_{a_{i-1}}^{a_i}s(x)dx.
$$
The simpler function can choose constant function 
$$c(x)$$, linear function $$l(x)$$ and quadratic function $$q(x)$$,
which give us *middle point rule*, *Trapezoidal's rule* and *Simpson's rule*, 
respectively.

### Middle Point Rule
Middle point rule use an constant function $$c_i(x)$$, which satisfy
$$c_i(x)=f(x_i), \quad \forall x \in {a_{i-1}, a_i}$$, to estimate the result
$$
I_n^M = \frac{h}{2}\sum_{i=1}^n (f(a_{i-1}) + f(a_i)).
$$

### Trapezoidal's Rule
Trapezoidal's rule use a linear function $$l_i(x)$$, 
which satisfy $$l_i(a_{i-1}) = f(a_{i-1}), \quad l_i(a_i) = f(a_i)$$, 
to approximate the result.

### Simpsom's Rule
Simpsom's rule use a quadratic function $$q_i(x)$$, which satisfy 
$$q_i(a_{i-1}) = f(a_{i-1}),\quad, q_i(x_i) = f(x_i),\quad q_i(a_i) = f(a_i)$$.

## the convergence
If the three result do not converge to the real result $$I$$, they have no meaning. If
$$
\lim_{n\to\infty}I_n = I
$$
The approximation is said to be converge.
