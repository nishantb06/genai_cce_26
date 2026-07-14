Definition 4.12

Let $X$ be an exponential random variable. The PDF of $X$ is

$$
f_X(x) =
\begin{cases}
\lambda e^{-\lambda x}, & x \geq 0, \\
0, & \text{otherwise},
\end{cases}
$$

where $\lambda > 0$ is a parameter. We write $X \sim \mathrm{Exponential}(\lambda)$ to mean that $X$ is drawn from an exponential distribution of parameter $\lambda$.

In this definition, the parameter $\lambda$ of the exponential random variable determines the rate of decay. A large $\lambda$ implies a faster decay.

![[Pasted image 20260712145420.png]]
The CDF of an exponential random variable can be determined by

$$
\begin{aligned}
F_X(x)
&= \int_{-\infty}^{x} f_X(t)\, dt \\
&= \int_{0}^{x} \lambda e^{-\lambda t}\, dt \\
&= 1 - e^{-\lambda x}, \quad x \geq 0.
\end{aligned}
$$

Therefore, if we consider the entire real line, the CDF is

$$
F_X(x) =
\begin{cases}
0, & x < 0, \\
1 - e^{-\lambda x}, & x \geq 0.
\end{cases}
$$


If $X \sim \mathrm{Exponential}(\lambda)$, then

$$\mathbb{E}[X] = \frac{1}{\lambda} \quad \text{and} \quad \mathrm{Var}[X] = \frac{1}{\lambda^2}.$$

**Proof.** We have discussed this proof before. Here is a recap for completeness:

$$
\begin{aligned}
\mathbb{E}[X]
&= \int_{-\infty}^{\infty} x\, f_X(x)\, dx \\
&= \int_{0}^{\infty} \lambda x e^{-\lambda x}\, dx \\
&= -\int_{0}^{\infty} x\, d\!\left(e^{-\lambda x}\right) \\
&= -x e^{-\lambda x}\Big|_{0}^{\infty} + \int_{0}^{\infty} e^{-\lambda x}\, dx \\
&= \frac{1}{\lambda},
\end{aligned}
$$

$$
\begin{aligned}
\mathbb{E}[X^2]
&= \int_{-\infty}^{\infty} x^2\, f_X(x)\, dx \\
&= \int_{0}^{\infty} \lambda x^2 e^{-\lambda x}\, dx \\
&= -\int_{0}^{\infty} x^2\, d\!\left(e^{-\lambda x}\right) \\
&= -x^2 e^{-\lambda x}\Big|_{0}^{\infty} + \int_{0}^{\infty} 2x e^{-\lambda x}\, dx \\
&= 0 + \frac{2}{\lambda}\,\mathbb{E}[X] \\
&= \frac{2}{\lambda^2}.
\end{aligned}
$$

Thus, $\mathrm{Var}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2 = \frac{1}{\lambda^2}$.

Exponential random variables are closely related to [[Poisson Random Variable]]. Recall that the definition of a Poisson random variable is a random variable that describes the number of events that happen in a certain period, e.g., photon arrivals, number of pedestrians, phone calls, etc. We summarize the origin of an exponential random variable as follows.

- An exponential random variable is the interarrival time between two consecutive Poisson events.
- That is, an exponential random variable is how much time it takes to go from $N$ Poisson counts to $N+1$ Poisson counts.


----
Origin of this RV

An example will clarify this concept. Imagine that you are waiting for a bus, as illustrated in Figure 4.21. Passengers arrive at the bus stop with an arrival rate $\lambda$ per unit time. Thus, for some time $t$, the average number of people that arrive is $\lambda t$. Let $N$ be a random variable denoting the number of people. We assume that $N$ is Poisson with a parameter $\lambda t$. That is, for any duration $t$, the probability of observing $n$ people follows the PMF

$$P[N=n] = \frac{(\lambda t)^n}{n!} e^{-\lambda t}.$$

![Figure 4.21](https://probability4datascience.com/eBook/pix/ch4_exp_inter_arrival.png)

**Figure 4.21.** For any fixed period of time $t$, the number of people $N$ is modeled as a Poisson random variable with a parameter $\lambda t$.

Let $T$ be the interarrival time between two people, by which we mean the time between two consecutive arrivals, as shown in Figure 4.22. Note that $T$ is a random variable because $T$ depends on $N$, which is itself a random variable. To find the PDF of $T$, we first find the CDF of $T$. We note that

$$
\begin{aligned}
P[T > t]
&= P[\text{interarrival time } > t] && \text{(a)} \\
&= P[\text{no arrival in } t] && \text{(b)} \\
&= P[N=0] && \text{(c)} \\
&= \frac{(\lambda t)^0}{0!} e^{-\lambda t} \\
&= e^{-\lambda t}.
\end{aligned}
$$

In this set of arguments, (a) holds because $T$ is the interarrival time, and (b) holds because interarrival time is between two consecutive arrivals. If the interarrival time is larger than $t$, there is no arrival during the period. Equality (c) holds because $N$ is the number of passengers.

![Figure 4.22](https://probability4datascience.com/eBook/pix/ch4_exp_inter_arrival_02.png)

**Figure 4.22.** The interarrival time $T$ between two consecutive Poisson events is an exponential random variable.

Since $P[T > t] = 1 - F_T(t)$, where $F_T(t)$ is the CDF of $T$, we can show that

$$
\begin{aligned}
F_T(t) &= 1 - e^{-\lambda t}, \\
f_T(t) &= \frac{d}{dt} F_T(t) = \lambda e^{-\lambda t}.
\end{aligned}
$$

Therefore, the interarrival time $T$ follows an exponential distribution.

Since exponential random variables are tightly connected to Poisson random variables, we should expect them to be useful for modeling temporal events. We discuss two examples.
