Suppose we flip the coin $n$ times and count the number of heads. Since each coin flip is a random variable ([[Bernoulli Random Variable | Bernoulli]]), the sum is also a random variable. It turns out that this new random variable is the binomial random variable.



---
Let $X$ be a binomial random variable. Then, the PMF of $X$ is

$$p_X(k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad k=0,1,\ldots,n,$$

where $0 < p < 1$ is the binomial parameter, and $n$ is the number of trials. We write $X \sim \mathrm{Binomial}(n,p)$ to say that $X$ is drawn from a binomial distribution with a parameter $p$ of size $n$.

---

#### Properties
If $X \sim \mathrm{Binomial}(n,p)$, then

$$
\begin{aligned}
\mathbb{E}[X] &= np, \\
\mathbb{E}[X^2] &= np\bigl(np + (1-p)\bigr), \\
\mathrm{Var}[X] &= np(1-p).
\end{aligned}
$$
