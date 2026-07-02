## Multivariate Gaussian distribution
> A random variable is said to be k-variate normally distributed if every linear combination of its k components have a univariate normal distribution.


> if all k components are independent Gaussian random variables, then  must be multivariate Gaussian (because the sum of independent Gaussian random variables is always Gaussian)

> sum of random variables is different from sum of distribution – the sum of two Gaussian distributions gives you a Gaussian mixture, which is not Gaussian except in special cases.

![[Pasted image 20260626103601.png]]
$$  
\mathbf{x} \sim \mathcal{N}(\boldsymbol{\mu}, \boldsymbol{\Sigma})  
$$

$$
p(\mathbf{x})
=
\frac{1}
{(2\pi)^{d/2} |\boldsymbol{\Sigma}|^{1/2}}
\exp\!\left(
-\frac{1}{2}
(\mathbf{x}-\boldsymbol{\mu})^\top
\boldsymbol{\Sigma}^{-1}
(\mathbf{x}-\boldsymbol{\mu})
\right)
$$

### Gaussian Distribution (Multivariate)

$$\mathcal{N}(x;\, \mu, \Sigma) = \frac{1}{(2\pi)^{d/2}|\Sigma|^{1/2}} \exp\!\left(-\frac{1}{2}(x-\mu)^\top \Sigma^{-1}(x-\mu)\right)$$

where $x \in \mathbb{R}^d$, $\mu \in \mathbb{R}^d$, $\Sigma \in \mathbb{R}^{d \times d}$.
