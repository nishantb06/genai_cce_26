The [[Isotropic or Standard Gaussian]] [[Cumulative Distribution Function (CDF)]] is related to a so-called error function defined as

$$
\mathrm{erf}(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-t^2}\, dt.
$$

It is easy to link $\Phi(x)$ with $\mathrm{erf}(x)$:

$$
\Phi(x) = \frac{1}{2}\left[1 + \mathrm{erf}\left(\frac{x}{\sqrt{2}}\right)\right],
\quad \text{and} \quad
\mathrm{erf}(x) = 2\Phi\left(x\sqrt{2}\right) - 1.
$$

With the standard Gaussian CDF, we can define the CDF of an arbitrary Gaussian.

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
