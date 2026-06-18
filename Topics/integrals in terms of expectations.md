To represent integral in terms of expectations
We need to understand this first 
$$\int p_X(x)\, g(x)\, dx = \mathbb{E}_{x \sim p_X}[\,g(x)\,]$$
Then this expectation can be approximated using the [[Weak Law of Large Numbers | WLLN]]

The probability density can also be a conditional probability density function. In that case x will be sample from a conditional probability density function

Integrals involving [[Probability Density]] functions can be approximated using samples drawn from the distribution

## Key Idea

> Integrals involving density functions can be approximated using samples drawn from the distribution.

---

## Setup

Suppose we want to compute the following integral:

$$I = \int_x h(x), p_x(x), dx$$

where $h(x)$ is an arbitrary function and $p_x(x)$ is the density function.

This is simply an expectation:

$$I = \mathbb{E}_{P_x}!\left[h(x)\right]$$

---

## Approximation via Samples

We have samples drawn iid from $P_x$:

$$x_1, x_2, \ldots, x_n \sim \text{iid } P_x$$

### Law of Large Numbers

$$\lim_{n \to \infty} \frac{1}{n} \sum_{i=1}^{n} h(x_i) \approx \mathbb{E}_{P_x}\left[h(x)\right], \quad x_i \sim \text{iid } P_x$$

---

## Connection to f-Divergence

If the [[F-Divergence]] can be expressed in terms of expectations over $p_x$, it can be approximated using the above.

---

## Tags

#monte-carlo #law-of-large-numbers #expectation #f-divergence #sampling #machine-learning

