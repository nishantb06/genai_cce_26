A Bernoulli random variable is a _coin-flip_ random variable. It has two states either 1 or 0
The random variable has two states: either 1 or 0. The probability of getting 1 is $p$, and the probability of getting 0 is $1-p$

Let $X$ be a Bernoulli random variable. Then, the PMF of $X$ is

$$p_X(0) = 1-p, \qquad p_X(1) = p,$$

where $0 < p < 1$ is called the Bernoulli parameter. We write $X \sim \mathrm{Bernoulli}(p)$ to say that $X$ is drawn from a Bernoulli distribution with a parameter $p$.


---

Properties of Bernoulli RV's
If $X \sim \mathrm{Bernoulli}(p)$, then

$$\mathbb{E}[X] = p, \qquad \mathbb{E}[X^2] = p, \qquad \mathrm{Var}[X] = p(1-p).$$


----
#### When will a Bernoulli random variable have the maximum variance?
When p = 0.5 as the variance of the RV is given by $p - p^2$ , which gets its maxima at 0.5


#### Erdos-Enri graph
In a collection of n nodes , if the probability of getting an edge is given by the Bernoulli RV then such a graph is called this


---
Suppose we flip the coin n times and count the number of heads. Since each coin flip is a random variable (Bernoulli), the sum is also a random variable. It turns out that this new random variable is the [[Binomial Random Variable]]

