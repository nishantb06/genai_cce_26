kurtosis is the fourth central moment of a [[Gaussian Random Variable]]

Kurtosis measures how heavy-tailed the distribution is. There are two forms of kurtosis: one is the standard kurtosis, which is the fourth central moment, and the other is the excess kurtosis, which is $\kappa_{\mathrm{excess}} = \kappa - 3$. The constant 3 comes from the kurtosis of a standard Gaussian. Excess kurtosis is more widely used in data analysis. The interpretation of kurtosis is the comparison to a Gaussian. If the excess kurtosis is positive, the distribution has a tail that decays more slowly than a Gaussian. If the excess kurtosis is negative, the distribution has a tail that decays faster than a Gaussian. Figure 4.29 illustrates the (excess) kurtosis of three different distributions.

- $\kappa = \mathbb{E}\left[\left(\dfrac{X-\mu}{\sigma}\right)^4\right]$.
- Measures how heavy-tailed the distribution is. Gaussian has kurtosis 3.
- Some statisticians prefer excess kurtosis $\kappa - 3$, so that Gaussian has excess kurtosis $0$.


On a computer, computing the empirical skewness and kurtosis is done by built-in commands. Their implementations are based on the finite-sample calculations

$$
\gamma \approx \frac{1}{N}\sum_{n=1}^{N}\left(\frac{X_n-\mu}{\sigma}\right)^3, \quad
\kappa \approx \frac{1}{N}\sum_{n=1}^{N}\left(\frac{X_n-\mu}{\sigma}\right)^4.
$$
