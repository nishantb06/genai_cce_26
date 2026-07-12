### For Discrete RV's
Let $X$ be a discrete random variable with $\Omega=\{x_1,x_2,\ldots\}$. The cumulative distribution function (CDF) of $X$ is

$$F_X(x_k) \stackrel{\mathrm{def}}{=} P[X \leq x_k] = \sum_{\ell=1}^{k} p_X(x_\ell).$$

If $\Omega=\{\ldots,-1,0,1,2,\ldots\}$, then the CDF of $X$ is

$$F_X(k) \stackrel{\mathrm{def}}{=} P[X \leq k] = \sum_{\ell=-\infty}^{k} p_X(\ell).$$

A CDF is essentially the cumulative sum of a PMF from $-\infty$ to $x$, where the variable $\ell$ in the sum is a dummy variable.

A CDF is a staircase function, that is it will always increase in steps if the RV is Discrete
. Second, the minimum value of a CDF is 0, whereas the maximum value is 1

Third, the gap at each jump is exactly the probability mass at that state. Let us summarize these observations in the following theorem.

If $X$ is a discrete random variable, then the CDF of $X$ has the following properties:

1. **(i)** The CDF is a sequence of increasing unit steps.
2. **(ii)** The maximum of the CDF is when $x=\infty$: $F_X(+\infty)=1$.
3. **(iii)** The minimum of the CDF is when $x=-\infty$: $F_X(-\infty)=0$.
4. **(iv)** The unit steps have jumps at positions where $p_X(x)>0$.

# For Continuous RV's
Let $X$ be a continuous random variable with a sample space $\Omega = \mathbb{R}$. The cumulative distribution function (CDF) of $X$ is

$$F_X(x) \stackrel{\mathrm{def}}{=} P[X \leq x] = \int_{-\infty}^{x} f_X(x')\, dx'.$$

Let $X$ be a random variable (either continuous or discrete), then the CDF of $X$ has the following properties:

1. **(i)** The CDF is nondecreasing.
2. **(ii)** The maximum of the CDF is when $x=\infty$: $F_X(+\infty)=1$.
3. **(iii)** The minimum of the CDF is when $x=-\infty$: $F_X(-\infty)=0$.


---
Let $X$ be a continuous random variable. If the CDF $F_X$ is continuous at any $a \leq x \leq b$, then

$$P[a \leq X \leq b] = F_X(b) - F_X(a).$$

**Proof.** The proof follows from the definition of the CDF, which states that

$$
\begin{aligned}
F_X(b) - F_X(a)
&= \int_{-\infty}^{b} f_X(x')\, dx' - \int_{-\infty}^{a} f_X(x')\, dx' \\
&= \int_{a}^{b} f_X(x')\, dx' \\
&= P[a \leq X \leq b].
\end{aligned}
$$

This result provides a very handy tool for calculating the probability of an event $a \leq X \leq b$ using the CDF.

---

#### Retrieving PDF from CDF

Thus far, we have only seen how to obtain $F_X(x)$ from $f_X(x)$. In order to go in the reverse direction, we recall the fundamental theorem of calculus. This states that if a function $f$ is continuous, then

$$f(x) = \frac{d}{dx} \int_{a}^{x} f(t)\, dt$$

for some constant $a$. Using this result for CDF and PDF, we have the following:

Theorem 4.5

The probability density function (PDF) is the derivative of the cumulative distribution function (CDF):

$$f_X(x) = \frac{d F_X(x)}{dx} = \frac{d}{dx} \int_{-\infty}^{x} f_X(x')\, dx',$$

provided $F_X$ is differentiable at $x$. If $F_X$ is not differentiable at $x = x_0$, then,

$$f_X(x) = P[X = x_0]\, \delta(x - x_0), \quad \text{when } x = x_0.$$

The CDF is always a well-defined function. It is integrable everywhere. If the underlying random variable is continuous, the CDF is also continuous. If the underlying random variable is discrete, the CDF is a staircase function.
