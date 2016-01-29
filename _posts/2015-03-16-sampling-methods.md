---
layout: post
disqus_comments: yes
title: "Sampling Methods"
---
Most probabilistic models in practice have no exact inference solution,
and so we have to resort to approximation. Besides variational inference,
a numerical approximation called *Monte Carlo* is widely used to conquer
inference problems.

## Monte Carlo Sampling
In many applications, we are intrested in the expectation of some function
$$f(z)$$ respect to a probability distribution $$p(z)$$. However, expectation 
expression

$$
E[f(z)] = \int f(z)p(z) dz
$$

is usually intractable. Monte Carlo methods try to draw a set of independent
samples $$z^{(l)}$$ (where $$l=1, 2, \dots, L$$), from the the distribution, and evaluate

$$
\hat{f}(z) = \frac{1}{L} \sum_{l=1}^L f(z^{(l)}),
$$

to approximate $$E[f(z)]$$ since $$E[\hat f(z)]=E[f(z)]$$.  The variance of
the estimator is given by

$$
var(\hat{f}(z)) = \frac{1}{L} E[(f(z) - E[f(z)])^2],
$$

so not too many samples are needed to  estimate an expectation to sufficient
accuracy.

## One-pass Sampling for Directed Probability Graph Models
In directed probabilistic graph models, the joint probability is specified by

$$
p(\mathbf{z}) = \prod_i p(\mathbf{z}_i | \pi_i),
$$

where $$\pi_i$$ denotes the set of $$\mathbf{z}_i$$'s parents. Each variable
can be sampled after its parents have been sampled. We can always find an order
, follow which we can sample each variable one-by-one and after take a one pass
through all the variables, we get a sample from the joint distribuiton.

If some variables have been obsevered, the above procedure could be altered
to drawn conditional samples, given the observed variables are discrete.
When sampling for an observed variable, we compare the sampled value to the observed
value. If they agree, then we continue to sample the remaining variables. However,
if they disagree, we discard all values we have sampled so far and start the algorithm
from the first node. This method has a severe problem of inefficiency since the
probability of accepting the sample decrease rapidly as the number of observed
varaibles increase and as the number of the number of states that those variables
can take increases. Thus this method is rarely applied in practice.

To sample a marginal distribution is easy after we have get samples from the joint probability.
When we have drawn a set of independ samples from joint distribution $$p(z,x)$$, to get
maginal distribution $$p(z)$$, we just need to discard values for $$x$$ in each sample.

