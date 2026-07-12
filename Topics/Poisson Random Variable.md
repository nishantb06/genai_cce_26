In many physical systems, the arrivals of events are typically modeled as a Poisson random variable, e.g., photon arrivals, electron emissions, and telephone call arrivals. In social networks, the number of conversations per user can also be modeled as a Poisson. In e-commerce, the number of transactions per paying user is again modeled using a Poisson.

Let $X$ be a Poisson random variable. Then, the PMF of $X$ is

$$p_X(k) = \frac{\lambda^k}{k!} e^{-\lambda}, \quad k=0,1,2,\ldots,$$

where $\lambda > 0$ is the Poisson rate. We write $X \sim \mathrm{Poisson}(\lambda)$ to say that $X$ is drawn from a Poisson distribution with a parameter $\lambda$.

In this definition, the parameter $\lambda$ determines the rate of the arrival. The histogram and PMF of a Poisson random variable are illustrated in Figure 3.32. Here, we assume that $\lambda=1$.

$\lambda$ is also called flux or the arrival rate.

Should read about the origin of the Poisson RV from [here](https://probability4datascience.com/eBook/ch03-5.html) 

---

Show that the Poisson PMF sums to 1.

Solution

We use the exponential series to prove this result:

$$
\begin{aligned}
\sum_{k=0}^{\infty} p_X(k)
&= \sum_{k=0}^{\infty} \frac{\lambda^k}{k!} e^{-\lambda} \\
&= e^{-\lambda} \sum_{k=0}^{\infty} \frac{\lambda^k}{k!} \\
&= e^{-\lambda} \cdot e^{\lambda} \\
&= 1.
\end{aligned}
$$
Uses [[Taylor Series]] for the approximation of the Infinite series

---

Properties

## Properties of a Poisson random variable

We now derive the mean and variance of a Poisson random variable.

Theorem 3.9

If $X \sim \mathrm{Poisson}(\lambda)$, then

$$
\begin{aligned}
\mathbb{E}[X] &= \lambda, \\
\mathbb{E}[X^2] &= \lambda + \lambda^2, \\
\mathrm{Var}[X] &= \lambda.
\end{aligned}
$$

---
#### [[Signal to Noise Ratio]] of a Poisson RV 
is $\sqrt{\lambda}$ as A Poisson random variable has a variance equal to the mean

---

#### Poisson approximation to the [[Binomial Random Variable]]

(Poisson approximation to binomial). For small $p$ and large $n$,

$$\binom{n}{k} p^k (1-p)^{n-k} \approx \frac{\lambda^k}{k!} e^{-\lambda},$$

where $\lambda \stackrel{\mathrm{def}}{=} np$.

**Proof.** Let $\lambda = np$. Then,

$$
\begin{aligned}
\binom{n}{k} p^k (1-p)^{n-k}
&= \frac{n!}{k!(n-k)!} \left(\frac{\lambda}{n}\right)^k \left(1-\frac{\lambda}{n}\right)^{n-k} \\
&= \frac{\lambda^k}{k!} \cdot \frac{n(n-1)\cdots(n-k+1)}{n \cdot n \cdots n} \left(1-\frac{\lambda}{n}\right)^{n-k} \\
&= \frac{\lambda^k}{k!} \underbrace{\left(1\right)\left(1-\frac{1}{n}\right)\cdots\left(1-\frac{k-1}{n}\right)}_{\to 1 \text{ as } n \to \infty} \underbrace{\left(1-\frac{\lambda}{n}\right)^{-k}}_{\to 1 \text{ as } n \to \infty} \left(1-\frac{\lambda}{n}\right)^{n} \\
&= \frac{\lambda^k}{k!} \left(1-\frac{\lambda}{n}\right)^{n}.
\end{aligned}
$$

We claim that $\left(1-\frac{\lambda}{n}\right)^{n} \to e^{-\lambda}$. This can be proved by noting that

$$\log(1+x) \approx x, \quad x \ll 1.$$

It then follows that $\log\left(1-\frac{\lambda}{n}\right) \approx -\frac{\lambda}{n}$. Hence, $\left(1-\frac{\lambda}{n}\right)^{n} \approx e^{-\lambda}$

Consider an optical communication system. The bit arrival rate is $10^{9}$ bits/sec, and the probability of having one error bit is $10^{-9}$. Suppose we want to find the probability of having five error bits in one second.

Let $X$ be the number of error bits. In one second there are $10^{9}$ bits. Since we do not know the location of these 5 bits, we have to enumerate all possibilities. This leads to a binomial distribution. Using the binomial distribution, we know that the probability of having $k$ error bits is

$$P[X=k] = \binom{n}{k} p^k (1-p)^{n-k} = \binom{10^{9}}{k} (10^{-9})^k (1-10^{-9})^{10^{9}-k}.$$

This quantity is difficult to calculate in floating-point arithmetic.

Using the Poisson approximation to the binomial, we can see that the probability can be approximated by

$$P[X=k] \approx \frac{\lambda^k}{k!} e^{-\lambda},$$

where $\lambda = np = 10^{9}(10^{-9}) = 1$. Setting $k=5$ yields $P[X=5] \approx 0.003$.
