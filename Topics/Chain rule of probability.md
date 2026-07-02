For random variables $x_0, x_1, \ldots, x_T$:

$$P(x_0, x_1, \ldots, x_T) = P(x_0 \mid x_1, \ldots, x_T)\, P(x_1, \ldots, x_T).$$

Applying this recursively,

$$
\begin{aligned}
P(x_0, \ldots, x_T) &= P(x_0 \mid x_1, \ldots, x_T) \\
&\quad \times P(x_1 \mid x_2, \ldots, x_T) \\
&\quad \times \cdots \\
&\quad \times P(x_{T-1} \mid x_T) \\
&\quad \times P(x_T).
\end{aligned}
$$

### Example with four variables

Suppose we have $A, B, C, D$.

The chain rule gives

$$P(A, B, C, D) = P(A \mid B, C, D)\, P(B \mid C, D)\, P(C \mid D)\, P(D).$$

Notice this is **always true**. No assumptions have been made.

----


$$
P(A,B,C \mid D)
=
P(A \mid B,C,D)\,
P(B \mid C,D)\,
P(C \mid D)
$$
From the [[Bayes Rule]] we can write 

$$
P(A,B,C \mid D)
=
\frac{P(A,B,C,D)}{P(D)}
$$
And from the section above we know this following equation
$$
P(A,B,C,D)
=
P(A \mid B,C,D)\,
P(B \mid C,D)\,
P(C \mid D)\,
P(D)
$$
Therefore substituting eq 3 in eq 2 we get eq 1

$$
P(X_1,\ldots,X_n)
=
\prod_{i=1}^{n}
P\!\left(
X_i
\mid
X_{i+1},\ldots,X_n
\right)
$$

$$
P(X_1,\ldots,X_n \mid Y)
=
\prod_{i=1}^{n}
P\!\left(
X_i
\mid
X_{i+1},\ldots,X_n,Y
\right)
$$
