A Gaussian random variable is a random variable $X$ such that its [[Probability Density Function|PDF]] is

$$
f_X(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left\{-\frac{(x-\mu)^2}{2\sigma^2}\right\},
$$

where $(\mu,\sigma^2)$ are parameters of the distribution. We write $X \sim \mathrm{Gaussian}(\mu,\sigma^2)$ or $X \sim \mathrm{N}(\mu,\sigma^2)$ to say that $X$ is drawn from a Gaussian distribution of parameter $(\mu,\sigma^2)$.

Gaussian random variables have two parameters $(\mu,\sigma^2)$. It is noteworthy that the mean is $\mu$ and the variance is $\sigma^2$ — these two parameters are exactly the first moment (Expectation) and the second central moment of the random variable. Most other random variables do not have this property.


Note also that if $\sigma$ is very small, it is possible that $f_X(x) > 1$ although the integration over $\Omega$ will still be 1.

[[Isotropic or Standard Gaussian]]
With the Standard Gaussian's CDF ,we can define CDF of any arbitrary Gaussian
Let $X \sim \mathrm{N}(\mu,\sigma^2)$. Then

$$
F_X(x) = \Phi\left(\frac{x-\mu}{\sigma}\right).
$$

**Proof.** We start by expressing $F_X(x)$:

$$
\begin{aligned}
F_X(x)
&= \mathrm{P}[X \leq x] \\
&= \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(t-\mu)^2}{2\sigma^2}}\, dt.
\end{aligned}
$$

Substituting $y = \dfrac{t-\mu}{\sigma}$, and using the definition of standard Gaussian, we have

$$
\begin{aligned}
&\int_{-\infty}^{x} \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(t-\mu)^2}{2\sigma^2}}\, dt \\
&= \int_{-\infty}^{\frac{x-\mu}{\sigma}} \frac{1}{\sqrt{2\pi}} e^{-\frac{y^2}{2}}\, dy \\
&= \Phi\left(\frac{x-\mu}{\sigma}\right).
\end{aligned}
$$


An immediate consequence of this result is that

$$
\mathrm{P}[a < X \leq b] = \Phi\left(\frac{b-\mu}{\sigma}\right) - \Phi\left(\frac{a-\mu}{\sigma}\right).
$$

To see this, note that

$$
\begin{aligned}
\mathrm{P}[a < X \leq b]
&= \mathrm{P}[X \leq b] - \mathrm{P}[X \leq a] \\
&= \Phi\left(\frac{b-\mu}{\sigma}\right) - \Phi\left(\frac{a-\mu}{\sigma}\right).
\end{aligned}
$$


Properties of the CDF of a Gaussian
Let $X \sim \mathrm{N}(\mu,\sigma^2)$. Then the following results hold:

- $\Phi(y) = 1 - \Phi(-y)$.
- $\mathrm{P}[X \geq b] = 1 - \Phi\left(\dfrac{b-\mu}{\sigma}\right)$.
- $\mathrm{P}[|X| \geq b] = 1 - \Phi\left(\dfrac{b-\mu}{\sigma}\right) + \Phi\left(\dfrac{-b-\mu}{\sigma}\right)$.

---
Higher order Moments
For a random variable $X$ with PDF $f_X(x)$, define the following central moments as

$$
\begin{aligned}
\text{mean} &= \mathbb{E}[X] = \mu, \\
\text{variance} &= \mathbb{E}[(X-\mu)^2] = \sigma^2,
\end{aligned}
$$

[[Skewness]] $= \mathbb{E}\left[\left(\dfrac{X-\mu}{\sigma}\right)^3\right] = \gamma$,

[[Kurtosis]] $= \mathbb{E}\left[\left(\dfrac{X-\mu}{\sigma}\right)^4\right] = \kappa$, excess kurtosis $\kappa-3$.

---
To read more on the origin of Gaussian RV read [[As we sum more random variables, the distribution of the sum will converge to a Gaussian]] 