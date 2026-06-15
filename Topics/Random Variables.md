
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
