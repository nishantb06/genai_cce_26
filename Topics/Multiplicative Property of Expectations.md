If $X$ and $Y$ are independent, then $\mathbb{E}[XY] = \mathbb{E}[X]\mathbb{E}[Y]$.

Yes. If $X$ and $Y$ are independent and the expectations exist (for example, $\mathbb{E}[|XY|] < \infty$), then

$$
\mathbb{E}[XY] = \mathbb{E}[X]\,\mathbb{E}[Y].
$$

The proof follows directly from the definition of independence.

For continuous random variables:

$$
\begin{aligned}
\mathbb{E}[XY]
&= \iint xy\, f_{X,Y}(x,y)\,dx\,dy.
\end{aligned}
$$

Since $X$ and $Y$ are independent,

$$
f_{X,Y}(x,y) = f_X(x)f_Y(y),
$$

so

$$
\begin{aligned}
\mathbb{E}[XY]
&= \iint xy\, f_X(x)f_Y(y)\,dx\,dy \\
&= \left(\int x f_X(x)\,dx\right)
\left(\int y f_Y(y)\,dy\right) \\
&= \mathbb{E}[X]\mathbb{E}[Y].
\end{aligned}
$$

The same argument works for discrete random variables:

$$
\begin{aligned}
\mathbb{E}[XY]
&= \sum_x \sum_y xy\, P(X=x,Y=y) \\
&= \sum_x \sum_y xy\, P(X=x)P(Y=y) \\
&= \left(\sum_x xP(X=x)\right)
\left(\sum_y yP(Y=y)\right) \\
&= \mathbb{E}[X]\mathbb{E}[Y].
\end{aligned}
$$

More generally, if $X$ and $Y$ are independent and $g$ and $h$ are measurable functions for which the expectations exist, then

$$
\boxed{\mathbb{E}[g(X)h(Y)] = \mathbb{E}[g(X)]\,\mathbb{E}[h(Y)].}
$$

This generalization is frequently used in probability and machine learning proofs.
