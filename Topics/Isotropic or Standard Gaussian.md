The standard Gaussian (or standard normal) random variable $X$ has a PDF

$$
f_X(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}}.
$$

That is, $X \sim \mathrm{N}(0,1)$ is a Gaussian with $\mu = 0$ and $\sigma^2 = 1$.


The CDF of the standard Gaussian is defined as the $\Phi(\cdot)$ function

$$
\Phi(x) \stackrel{\mathrm{def}}{=} F_X(x) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{x} e^{-\frac{t^2}{2}}\, dt.
$$


The standard Gaussian's CDF is related to a so-called [[Error Function]] defined as

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
