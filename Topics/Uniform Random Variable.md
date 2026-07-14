Let $X$ be a continuous uniform random variable. The PDF of $X$ is

$$
f_X(x) =
\begin{cases}
\dfrac{1}{b-a}, & a \leq x \leq b, \\
0, & \text{otherwise},
\end{cases}
$$

where $[a,b]$ is the interval on which $X$ is defined. We write $X \sim \mathrm{Uniform}(a,b)$ to mean that $X$ is drawn from a uniform distribution on an interval $[a,b]$.


The CDF of a uniform random variable can be determined by integrating $f_X(x)$:

$$
\begin{aligned}
F_X(x)
&= \int_{-\infty}^{x} f_X(t)\, dt \\
&= \int_{a}^{x} \frac{1}{b-a}\, dt \\
&= \frac{x-a}{b-a}, \quad a \leq x \leq b.
\end{aligned}
$$

Therefore, the complete CDF is

$$
F_X(x) =
\begin{cases}
0, & x < a, \\
\dfrac{x-a}{b-a}, & a \leq x \leq b, \\
1, & x > b.
\end{cases}
$$


If $X \sim \mathrm{Uniform}(a,b)$, then

$$\mathbb{E}[X] = \frac{a+b}{2} \quad \text{and} \quad \mathrm{Var}[X] = \frac{(b-a)^2}{12}.$$

**Proof.** We have derived these results before. Here is a recap for completeness:

$$
\begin{aligned}
\mathbb{E}[X]
&= \int_{-\infty}^{\infty} x\, f_X(x)\, dx
= \int_{a}^{b} \frac{x}{b-a}\, dx
= \frac{a+b}{2}, \\
\mathbb{E}[X^2]
&= \int_{-\infty}^{\infty} x^2\, f_X(x)\, dx
= \int_{a}^{b} \frac{x^2}{b-a}\, dx
= \frac{a^2 + ab + b^2}{3}, \\
\mathrm{Var}[X]
&= \mathbb{E}[X^2] - \mathbb{E}[X]^2
= \frac{(b-a)^2}{12}.
\end{aligned}
$$
