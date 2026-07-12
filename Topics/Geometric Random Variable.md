In some applications, we are interested in trying a binary experiment until we succeed. For example, we may want to keep calling someone until the person picks up the call. In this case, the random variable can be defined as the outcome of many failures followed by a final success. This is called the geometric random variable.

Let $X$ be a geometric random variable. Then, the PMF of $X$ is

$$p_X(k) = (1-p)^{k-1} p, \quad k=1,2,\ldots,$$

where $0 < p < 1$ is the geometric parameter. We write $X \sim \mathrm{Geometric}(p)$ to say that $X$ is drawn from a geometric distribution with a parameter $p$.

We define it as [[Bernoulli Random Variable|Bernoulli]] trials with $k-1$ consecutive failures followed by one success. This can be seen from the definition:


--- 
Show that the geometric PMF sums to one.

Solution

We can apply infinite series to show the result:

$$
\begin{aligned}
\sum_{k=1}^{\infty} p_X(k)
&= \sum_{k=1}^{\infty} (1-p)^{k-1} p \\
&= p \cdot \sum_{k=1}^{\infty} (1-p)^{k-1}, \quad \ell = k-1 \\
&= p \cdot \sum_{\ell=0}^{\infty} (1-p)^{\ell} \\
&= p \cdot \frac{1}{1-(1-p)} \\
&= 1.
\end{aligned}
$$


----

Properties
If $X \sim \mathrm{Geometric}(p)$, then

$$
\begin{aligned}
\mathbb{E}[X] &= \frac{1}{p}, \\
\mathbb{E}[X^2] &= \frac{2}{p^2} - \frac{1}{p}, \\
\mathrm{Var}[X] &= \frac{1-p}{p^2}.
\end{aligned}
$$
