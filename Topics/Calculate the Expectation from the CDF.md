To calculate the [[Expectations]] from the [[Cumulative Distribution Function (CDF)]]

Lemma 4.1

Let $X > 0$. Then $\mathbb{E}[X]$ can be computed from $F_X$ as

$$\mathbb{E}[X] = \int_0^{\infty} (1 - F_X(t))\, dt.$$

**Proof.** The trick is to change the integration order:

$$
\begin{aligned}
\int_0^{\infty} (1 - F_X(t))\, dt
&= \int_0^{\infty} \bigl[1 - P[X \leq t]\bigr]\, dt \\
&= \int_0^{\infty} P[X > t]\, dt \\
&= \int_0^{\infty} \int_t^{\infty} f_X(x)\, dx\, dt \\
&= \int_0^{\infty} \int_0^{x} f_X(x)\, dt\, dx && \text{(a)} \\
&= \int_0^{\infty} \left(\int_0^{x} dt\right) f_X(x)\, dx \\
&= \int_0^{\infty} x\, f_X(x)\, dx \\
&= \mathbb{E}[X].
\end{aligned}
$$

![[Pasted image 20260712115903.png]]
![[Pasted image 20260712115911.png]]


Let $X < 0$. Then $\mathbb{E}[X]$ can be computed from $F_X$ as

$$\mathbb{E}[X] = -\int_{-\infty}^{0} F_X(t)\, dt.$$

The mean of a random variable $X$ can be computed from the CDF as

$$\mathbb{E}[X] = \int_0^{\infty} (1 - F_X(t))\, dt - \int_{-\infty}^{0} F_X(t)\, dt.$$

**Proof.** For any random variable $X$, we can partition $X = X^{+} - X^{-}$ where $X^{+}$ and $X^{-}$ are the positive and negative parts, respectively. Then, the above two lemmas will give us

$$
\begin{aligned}
\mathbb{E}[X] = \mathbb{E}[X^{+} - X^{-}]
&= \mathbb{E}[X^{+}] - \mathbb{E}[X^{-}] \\
&= \int_0^{\infty} (1 - F_X(t))\, dt - \int_{-\infty}^{0} F_X(t)\, dt.
\end{aligned}
$$

■

As illustrated in Figure 4.18, this equation is equivalent to computing the areas above and below the CDF and taking the difference.

![Figure 4.18](https://probability4datascience.com/eBook/pix/ch4_mean_2.png)

**Figure 4.18.** The mean of a random variable $X$ can be calculated by computing the area in the CDF.

How to find the mean from the CDF

- A formula is given by Eq.&nbsp;(4.20):
    
    $$\mathbb{E}[X] = \int_0^{\infty} (1 - F_X(t))\, dt - \int_{-\infty}^{0} F_X(t)\, dt.$$

- This result is not commonly used, but the proof technique of [[Switching the integration order]] is important
