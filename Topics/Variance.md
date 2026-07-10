> The variance of a random variable $X$ is
>
> $$\mathrm{Var}[X] = \mathbb{E}[(X - \mu)^2],$$
>
> where $\mu = \mathbb{E}[X]$ is the expectation of $X$.

We denote $\sigma^2$ by $\mathrm{Var}[X]$. The square root of the variance, $\sigma$, is called the standard deviation of $X$. Like the expectation $\mathbb{E}[X]$, the variance $\mathrm{Var}[X]$ is computed using the ideal histogram PMF. It is the limiting object of the usual standard deviation we calculate from a dataset.

It is the Second [[Moment]] of the [[Random Variables | RV]]    $X-\mathbb{E}[X]$ 

What does the variance mean? It is a measure of the _deviation_ of the random variable $X$ relative to its mean. This deviation is quantified by the squared difference $(X - \mu)^2$. The expectation operator takes the average of the deviation, giving us a deterministic number $\mathbb{E}[(X - \mu)^2]$.

--- 
#### Properties
The variance of a random variable $X$ has the following properties:

1. **(i)** Moment.
$$\mathrm{Var}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2.$$
2. **(ii)** Scale. For any constant $c$,
$$\mathrm{Var}[cX] = c^2\,\mathrm{Var}[X].$$
3. **(iii)**    DC Shift. For any constant $c$,
$$\mathrm{Var}[X + c] = \mathrm{Var}[X].$$
