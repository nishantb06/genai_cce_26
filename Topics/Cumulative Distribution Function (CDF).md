### For Discrete
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
