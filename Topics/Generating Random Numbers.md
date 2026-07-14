Computing software can easily generate random numbers, most commonly from a [[Uniform Random Variable|Uniform]] distribution. They can also generate Random Numbers from [[Gaussian Random Variable|Gaussian]] or Exponential random numbers. But how do we get it to generate random numbers from any arbitrary distribution.

#### General Principle
Generating random numbers according to the desired distribution can be formulated as an inverse problem. Suppose that we can generate uniformly random numbers according to Uniform(0,1). This is a fair assumption, and this process can be done on almost all computers today. Let us call this random variable $U$ and its realization $u$. Suppose that we also have a desired distribution $f_X(x)$ (and its CDF $F_X(x)$). We can put the two random variables $U$ and $X$ on the two axes of Figure 4.36, yielding an input-output relationship. The inverse problem is: By using what transformation $g$, such that $X = g(U)$, can we make sure that $X$ is distributed according to $f_X(x)$ (or $F_X(x)$)?

![[Pasted image 20260714143855.png]]

In short we assume that we can sample fairly from a Uniform Distribution, what transformation can we learn so that this sample from a Uniform distribution is transformed into a sample which seems like it is drawn from our target distribution ?


The transformation $g$ that can turn a uniform random variable into a random variable following a distribution $F_X(x)$ is given by

$$
g(u) = F_X^{-1}(u).
$$

That is, if $g = F_X^{-1}$, then $g(U)$ will be distributed according to $f_X$ (or $F_X$).

**Proof.** First, we know that if $U \sim \mathrm{Uniform}(0,1)$, then $f_U(u) = 1$ for $0 \leq u \leq 1$, so

$$
F_U(u) = \int_{-\infty}^{u} f_U(u')\, du' = u,
$$

for $0 \leq u \leq 1$. Let $g = F_X^{-1}$ and define $Y = g(U)$. Then the CDF of $Y$ is

$$
\begin{aligned}
F_Y(y)
&= \mathrm{P}[Y \leq y]
= \mathrm{P}[g(U) \leq y]
= \mathrm{P}[F_X^{-1}(U) \leq y] \\
&= \mathrm{P}[U \leq F_X(y)]
= F_X(y).
\end{aligned}
$$

Therefore, we have shown that the CDF of $Y$ is the CDF of $X$.


- Step 1: Generate a random number $U \sim \mathrm{Uniform}(0,1)$.
- Step 2: Let

$$
Y = F_X^{-1}(U).
$$

Then the distribution of $Y$ is $F_X$.

In Short , first generate Random numbers from a Uniform distribution between 0 and 1 then pass it through the Inverse of the [[Cumulative Distribution Function (CDF)|CDF]] of our target distribution.

This is what we also see in [[Sampling from a distribution]] in CCE course's notes

---
The above concept was present in [[DDPM Original Paper | Tutorial by Stanley Chan]] 

>Imagine that we are given a distribution p(x) and we want to draw samples from p(x). If x is a onedimensional variable, we can achieve the goal easily by inverting the cumulative distribution function (CDF) [7, Chapter 4] and sending a uniform[0, 1] random variable through this inverted CDF. For high dimensional distributions, the same CDF technique does not apply. However, the intuition of giving a higher weight to samples with a higher probability remains valid.
