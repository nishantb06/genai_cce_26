Given a random variable $X$ with PDF $f_X(x)$ and CDF $F_X(x)$, and supposing that $Y = g(X)$ for some function $g$, what are $f_Y(y)$ and $F_Y(y)$?

#### General Principle
Suppose we are given a random variable $X$ with PDF $f_X(x)$ and CDF $F_X(x)$. Let $Y = g(X)$ for some known and fixed function $g$. For simplicity, we assume that $g$ is monotonically increasing. In this case, the CDF of $Y$ can be determined as follows.

$$
\begin{aligned}
F_Y(y)
&\stackrel{(a)}{=} \mathrm{P}[Y \leq y] \\
&\stackrel{(b)}{=} \mathrm{P}[g(X) \leq y] \\
&\stackrel{(c)}{=} \mathrm{P}[X \leq g^{-1}(y)] \\
&\stackrel{(d)}{=} F_X(g^{-1}(y)).
\end{aligned}
$$


It will be useful to visualize the situation in Figure 4.34. Here, we consider a uniformly distributed $X$ so that the CDF $F_X(x)$ is a straight line. According to $F_X$, any samples drawn according to $F_X$ are equally likely, as illustrated by the yellow dots on the $x$-axis. As we transform the $X$'s through $Y = g(X)$, we increase/decrease the spacing between two samples. Therefore, some samples become more concentrated while some become less concentrated. The distribution of these transformed samples (the yellow dots on the $y$-axis) forms a new CDF $F_Y(y)$. The result $F_Y(y) = F_X(g^{-1}(y))$ holds when we look at $Y$. The samples are traveling with $g^{-1}$ in order to go back to $F_X$. Therefore, we need $g^{-1}$ in the formula.

![Figure 4.34](https://probability4datascience.com/eBook/pix/ch4_transform_01.png)
Why should we use the CDF and not the PDF in Figure 4.34? The advantage of the CDF is that it is an increasing function. Therefore, no matter what the function $g$ is, the input and the output functions will still be increasing. If we use the PDF, then the non-monotonic behavior of the PDF will interact with another nonlinear function $g$. It becomes much harder to decouple the two.

We can carry out the integrations to determine $F_X(g^{-1}(y))$. It can be shown that

$$
F_X(g^{-1}(y)) = \int_{-\infty}^{g^{-1}(y)} f_X(x')\, dx',
$$

and hence, by the fundamental theorem of calculus, we have

$$
\begin{aligned}
f_Y(y)
&= \frac{d}{dy} F_Y(y)
= \frac{d}{dy} F_X(g^{-1}(y)) \\
&= \frac{d}{dy} \int_{-\infty}^{g^{-1}(y)} f_X(x')\, dx'
= \left(\frac{d}{dy} g^{-1}(y)\right) \cdot f_X(g^{-1}(y)),
\end{aligned}
$$

where the last step is due to the chain rule. Based on this line of reasoning we can summarize a “recipe” for this problem.


- Step 1: Find the CDF $F_Y(y)$, which is $F_Y(y) = F_X(g^{-1}(y))$.
- Step 2: Find the PDF $f_Y(y)$, which is $f_Y(y) = \left(\dfrac{d}{dy} g^{-1}(y)\right) \cdot f_X(g^{-1}(y))$.

This recipe works when $g$ is a one-to-one mapping. If $g$ is not one-to-one, e.g., $g(x) = x^2$ implies $g^{-1}(y) = \pm\sqrt{y}$, then we will have some issues with the above two steps. When this happens, then instead of writing $X \leq g^{-1}(y)$ we need to determine the set $\{x \mid g(x) \leq y\}$.


The above are the principles which are used when [[Transforming one Random Variable into the other]] and also useful in the [[Reparameterization Trick]] 


https://probability4datascience.com/eBook/ch04-7.html
Read this when you want to see what happens when we do a Linear (AX+B) kind of transformation on [[Gaussian Random Variable]] , [[Exponential Random Variables]] etc

Note that $Y = X^2$ is a special case as this is not a 1-to-1 mapping, we deal with this separately, as seen in this article
