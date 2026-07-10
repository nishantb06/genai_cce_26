Random variables are mappings that translate events to numbers. After the translation, we have a set of numbers denoting the states of the random variables. Each state has a different probability of occurring. The probabilities are summarized by a function known as the probability mass function (PMF).

The **probability mass function (PMF)** of a random variable $X$ is a function which specifies the probability of obtaining a number $X(\xi) = x$. We denote a PMF as

$$p_X(x) = P[X = x]$$

The set of all possible states of $X$ is denoted as $X(\Omega)$.

Do not get confused by the sample space $\Omega$ and the set of states $X(\Omega)$. The sample space $\Omega$ contains all the possible outcomes of the experiments, whereas $X(\Omega)$ is the translation by the mapping $X$. The event $X = a$ is the set $X^{-1}(a) \subseteq \Omega$. Therefore, when we say $P[X = x]$ we really mean $P[X^{-1}(x)]$.

The probability mass function is a histogram summarizing the probability of each of the states $X$ takes. Since it is a histogram, a PMF can be easily drawn as a bar chart.

The PMF is the weighting function for discrete random variables. Two random variables are different when their PMFs are different because they are constructing two different [[Probability measure]]s.

A PMF should satisfy the condition that

$$\sum_{x \in X(\Omega)} p_X(x) = 1.$$

Next read [[Cumulative Distribution Function (CDF)]]
