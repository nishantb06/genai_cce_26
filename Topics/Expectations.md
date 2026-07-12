The expectation of a [[Random Variables | RV]] X is
$$
\mathbb{E}[X] = \sum_{x\in X(\Omega)} x\, p_X(x)
$$
Expectation is the mean of the RV $X$
Intuitively, we can think of $p_X(x)$ as the percentage of times that the random variable $X$ attains the value $x$. When this percentage is multiplied by $x$, we obtain the contribution of each $x$. Summing over all possible values of $x$ then yields the mean

The difference between $\mathbb{E}[X]$ and the average is that $\mathbb{E}[X]$ is computed from the _ideal_ histogram. For example we throw a dice milllion times , the histogram we get wont be ideal , but while calculating the Expectations we consider an Ideal histogram. When the number of samples $N$ approaches infinity, we expect the average to approximate $\mathbb{E}[X]$.

On the real line, the expectation can be regarded as the center of mass, which is the point where the “forces” between the two states are “balanced”.

---
#### Does every PMF have an expectation
No, because we can construct a PMF such that the expectation is undefined.
Consider a random variable $X$ with the following PMF:

$$p_X(k) = \frac{6}{\pi^2 k^2}, \quad k=1,2,\ldots.$$

Using a result from algebra, one can show that $\sum_{k=1}^{\infty} \frac{1}{k^2} = \frac{\pi^2}{6}$. Therefore, $p_X(k)$ is a legitimate PMF because $\sum_{k=1}^{\infty} p_X(k) = 1$. However, the expectation diverges, because

$$\mathbb{E}[X] = \sum_{k=1}^{\infty} k\, p_X(k) = \frac{6}{\pi^2} \sum_{k=1}^{\infty} \frac{1}{k} \to \infty,$$

where the divergence is due to the harmonic series ([https://en.wikipedia.org/wiki/Harmonic_series_(mathematics)](https://en.wikipedia.org/wiki/Harmonic_series_(mathematics))): $1 + \frac{1}{2} + \frac{1}{3} + \cdots = \infty$.

---
### Properties of expectations

The expectation of a random variable $X$ has the following properties:

1. **(i)**
    Function. For any function $g$,
$$\mathbb{E}[g(X)] = \sum_{x \in X(\Omega)} g(x)\, p_X(x).$$
2. **(ii)**
    Additive. For any function $g$ and $h$,
    $$\mathbb{E}[g(X) + h(X)] = \mathbb{E}[g(X)] + \mathbb{E}[h(X)].$$
3. **(iii)**
    Scale. For any constant $c$,
$$\mathbb{E}[cX] = c\,\mathbb{E}[X].$$
4. **(iv)**
DC Shift. For any constant $c$,
$$\mathbb{E}[X + c] = \mathbb{E}[X] + c.$$

[[Linear property of expected values]]
[[Multiplicative Property of Expectations]]

Based on the Concepts of expectations, we can define [[Moment]] and [[Variance]]