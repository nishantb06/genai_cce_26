Also called law of Iterated expectations, Tower rule , Adams law 

$$
\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[ X | Y]]
$$
Note the LHS , the First expectation iterates over all values of Y and in the inner [[Conditional expectation]], it iterates over all values of X given that y = Y.

Joint density : $f_{X,Y}(x,y)$
Marginal densities = $f_X(x)$ and $f_Y(y)$
Conditional density = $f_{X|Y}(x|y)$

and we know that 
$$
f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}
$$


conditional expectation is

$$E[X \mid Y=y] = \int_{-\infty}^{\infty} x, f_{X|Y}(x|y), dx.$$
Writing LHS in terms of integrals

$$\begin{aligned} E[E(X \mid Y)] &= \int_{-\infty}^{\infty} E(X \mid Y=y)\, f_Y(y)\, dy \ &= \int_{-\infty}^{\infty} \left( \int_{-\infty}^{\infty} x\, f_{X|Y}(x|y)\, dx \right) f_Y(y)\, dy \end{aligned}$$

Fubini's (or Tonelli's) theorem allows us to interchange the order of integration:

$$= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x, f_{X|Y}(x|y), f_Y(y), dy, dx.$$


Using the definition of conditional density,

$$f_{X|Y}(x|y)\, f_Y(y) = f_{X,Y}(x,y)\,$$

we get

$$= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x, f_{X,Y}(x,y)\, dy\, dx.$$

Since

$$f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)\, dy\,$$

we get

$$= \int_{-\infty}^{\infty} x\, f_X(x)\, dx = E(X).$$

Thus,

$$\boxed{E[E(X \mid Y)] = E(X).}$$