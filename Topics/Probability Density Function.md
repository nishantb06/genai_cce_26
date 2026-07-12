
Given a true distribution $P_X$ with density $p_X(x)$ and a model $P_\theta$ with density $p_\theta(x)$:

$$\int_{\mathcal{X}} p_X(x)\, dx = 1 \quad \text{(valid probability measure)}$$

> Note: $p_\theta(x)$ is the *[[Likelihood|likelihood]]* of $x$ under $\theta$, not necessarily a probability measure by itself.

In the example where we flip a fair coin twice, the pmf is

pX(0) = P[{(T,T)}] = 1/4
pX(1) = P[{(T,H),(H,T)}] = 2/4 ,
and pX(2) = P[{(H,H)}] = 1/4 ,

Note that this satisfies the above discretized version of the integral. 

The pmf can be represented by a histogram, or some parametric function (see Section 2.2.1). We call pX the probability distribution for the [[Random Variables]] X

The corresponding Cumulative density function would be 
pX(x<=0) = 1/4
pX(x<=1) = 3/4
pX(x<=2) = 1

----

Coming from the idea that [[Probability is a measure of the size or weight or volume of a set]] how do we measure the "size" of a continuous set? One possible way is by means of integrating the length, area, or volume covered by the set.

Therefore, we have translated the “size” of a set to an integration.

However, this definition is a very special case because when we calculate the “size” of a set, we treat all the elements in the set with equal importance. This is a strong assumption that will be relaxed later. But if you agree with this line of reasoning, we can rewrite the probability as

$$P[\{x \in A\}] = \frac{\int_A dx}{\int_\Omega dx} = \frac{\int_A dx}{|\Omega|} = \int_A \underbrace{\frac{1}{|\Omega|}}_{\text{equally important over } \Omega}\, dx.$$

What happens if we want to relax the “equiprobable” assumption? Perhaps we can adopt something similar to the probability mass function (PMF). Recall that a PMF $p_X$ evaluated at a point $x$ is the probability that the state $x$ happens, i.e., $p_X(x) = P[X=x]$. So, $p_X(x)$ is the relative frequency of $x$. Following the same line of thinking, we can define a function $f_X$ such that $f_X(x)$ tells us something related to the “relative frequency”. To this end, we can treat $f_X$ as a continuous histogram with infinitesimal bin width as shown in Figure 4.2. Using this $f_X$, we can replace the constant function $1/|\Omega|$ with the new function $f_X(x)$. This will give us

$$P[\{x \in A\}] = \int_A \underbrace{f_X(x)}_{\text{replace } 1/|\Omega|}\, dx.$$

Hence, $f_X$ can be considered a continuous version of $p_X$, although we do not recommend this way of thinking for the following reason: $p_X(x)$ is a legitimate probability, but $f_X(x)$ is not a probability. Rather, $f_X$ is the probability per unit length, meaning that we need to integrate $f_X$ (times $dx$) in order to generate a probability value. If we only look at $f_X$ at a point $x$, then this point is a measure-zero set because the length of this set is zero. This again links to the idea that [[Likelihood]] is not a probability measure but we get probability when we integrate PDF over some length

To summarize, we have learned that when measuring the size of a continuous event, the discrete technique (counting the number of elements) does not work. Generalizing to continuous space requires us to integrate the event. However, since different elements in an event have different relative emphases, we use the probability density function $f_X(x)$ to tell us the relative frequency for a state $x$ to happen. This PDF serves the role of the PMF.


---

Properties
A probability density function $f_X$ of a random variable $X$ is a mapping $f_X: \Omega \to \mathbb{R}$, with the properties

- Non-negativity: $f_X(x) \geq 0$ for all $x \in \Omega$
- Unity: $\int_\Omega f_X(x)\, dx = 1$
- Measure of a set: $P[\{x \in A\}] = \int_A f_X(x)\, dx$

**Remark**. Since isolated points have zero measure in the continuous space, the probability of an open interval $(a,b)$ is the same as the probability of a closed interval:

$$P[[a,b]] = P[(a,b)] = P[(a,b]] = P[[a,b)].$$

