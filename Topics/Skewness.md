skewness is the third central moment of a [[Gaussian Random Variable]]

Skewness measures the asymmetry of the distribution. Figure 4.28 shows three different distributions: one with left skewness, one with right skewness, and one symmetric. The skewness of a curve is

- Skewed towards left: negative
- Skewed towards right: positive
- Symmetric: zero


- $\mathbb{E}\left[\left(\dfrac{X-\mu}{\sigma}\right)^3\right]$.
- Measures the asymmetry of the distribution.


On a computer, computing the empirical skewness and kurtosis is done by built-in commands. Their implementations are based on the finite-sample calculations

$$
\gamma \approx \frac{1}{N}\sum_{n=1}^{N}\left(\frac{X_n-\mu}{\sigma}\right)^3, \quad
\kappa \approx \frac{1}{N}\sum_{n=1}^{N}\left(\frac{X_n-\mu}{\sigma}\right)^4.
$$
