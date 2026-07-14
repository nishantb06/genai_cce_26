To further illustrate the behavior of skewness and kurtosis, we consider an example using the gamma random variable $X$. The PDF of $X$ is given by the equation

$$
f_X(x) = \frac{1}{\Gamma(k)\theta^k} x^{k-1} e^{-x/\theta},
$$

where $\Gamma(\cdot)$ is known as the gamma function. If $k$ is an integer, the gamma function is just the factorial: $\Gamma(k) = (k-1)!$. A gamma random variable is parametrized by two parameters $(k,\theta)$. As $k$ increases or decreases, the shape of the PDF will change. For example, when $k=1$, the distribution is simplified to an exponential distribution.

Without going through the (tedious) integration, we can show that the skewness and the (excess) kurtosis of $\mathrm{Gamma}(k,\theta)$ are

$$
\begin{aligned}
\text{skewness} &= \frac{2}{\sqrt{k}}, \\
\text{(excess) kurtosis} &= \frac{6}{k}.
\end{aligned}
$$

As we can see from these results, the skewness and kurtosis diminish as $k$ grows. This can be confirmed from the PDF of $\mathrm{Gamma}(k,\theta)$ as shown in Figure 4.30.

![Figure 4.30](https://probability4datascience.com/eBook/pix/ch4_gamma.png)
