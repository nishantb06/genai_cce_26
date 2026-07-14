The random variable X is a _function_. The input to the function is an outcome of the sample space, whereas the output is a number on the real line. This type of function is somewhat different from an ordinary function that often translates a number to another number. Nevertheless, X is a function.

Elements of $\Omega$ are often inaccessible directly. We convert outcomes into real numbers via a **Random Variable (RV)**:

$$X : \Omega \to \mathbb{R}$$

**Example:**
$$\Omega = \{\text{conduct an X-ray}\}$$
$$X : \Omega \to \mathbb{R}^n, \quad n \in \mathbb{R}$$

**Random variable is not a variable but it is a function !**
It maps elements of the sample space to a real number. Domain of the function which is called the Random variable is an element of the event space and the Range can be higher dimensional space 
### Distribution of $X$

$$P_X(a) := P(X^{-1}((-\infty, a])) = P(\{\omega : X(\omega) \leq a\})$$

> Knowing $P_X(a)$ completely specifies the distribution.

**Example (die):**
$$\Omega = \{1,2,3,4,5,6\}, \quad P_X(u) = P(X^{-1}((-\infty, u]))$$

### Images as Data Points

An image of size $300 \times 200 \times 3$ is a vector in $\mathbb{R}^{180000}$.

Every data point is an element of the **range space** of the RV $X$.

$$P_X\!\left((-\infty, a_1] \times (-\infty, a_2] \times \cdots\right), \quad \mathbf{a} = [a_1, a_2, \ldots, a_d]$$

----

A random variable is a mapping from a statement to a number. However, we are now facing another difficulty. We knew how to measure the size of an event using the probability law $P$ because $P(\cdot)$ takes an event $E \in \mathcal{F}$ and sends it to a number between $[0,1]$. After the translation $X$, we cannot send the output $X(\xi)$ to $P(\cdot)$ because $P(\cdot)$ "eats" a set $E \in \mathcal{F}$ and not a number $X(\xi) \in \mathbb{R}$. Therefore, when we write $P[X=1]$, how do we measure the size of the event $X=1$?

This question appears difficult but is actually quite easy to answer. Since the probability law $P(\cdot)$ is always applied to an event, we need to define an event for the random variable $X$. If we write the sets clearly, we note that "$X=a$" is equivalent to the set

$$E = \{\xi \in \Omega \mid X(\xi) = a\}.$$

This is the set that contains all possible $\xi$'s such that $X(\xi)=a$. Therefore, when we say "find the probability of $X=a$," we are effectively asking the size of the set $E = \{\xi \in \Omega \mid X(\xi) = a\}$.

How then do we measure the size of $E$? Since $E$ is a subset in the sample space, $E$ is measurable by $P$. All we need to do is to determine what $E$ is for a given $a$. This, in turn, requires us to find the pre-image $X^{-1}(a)$, which is defined as

$$X^{-1}(a) \stackrel{\mathrm{def}}{=} \{\xi \in \Omega \mid X(\xi) = a\}.$$

Wait a minute, is this set just equal to $E$? Yes, the event $E$ we are seeking is exactly the pre-image $X^{-1}(a)$. As such, the probability measure of $E$ is

$$P[X=a] = P[X^{-1}(a)].$$

Next read [[Probability Mass Functions (PMF)]] for Discrete Random Variables. 

Next read [[Common Discrete Random Variables]] , [[Common Continuous Random Variable]]
 