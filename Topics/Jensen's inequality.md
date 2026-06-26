The fact that the [[F-Divergence]] distance metric has to be greater than zero is called jensens inequality. This is what leads to the face that the f function has to be convex

For any concave function (such as $\log$):

$$\log \mathbb{E}[\cdot] \geq \mathbb{E} \log[\cdot]$$
## Proof of Jensens Inequality

From [[Convex functions]] we know that the entire function lies above the tangent at any point
Let that point be $X_o$ . Let $X$ be a point some distance away from $X_o$ . then we can write
$$
f(x) > f(x_o) + m (x-x_o)
$$
where m is the slope of the function at $X_o$
Taking expectation on both sides
$$
\mathbb{E}(f(x)) > \mathbb{E}(f(x_o) + m (x-x_o))
$$
Using the [[Expectations | Linear rule for expectations]] . (Twice)

$$
\mathbb{E}(f(x)) > \mathbb{E}(f(x_o)) + m \,\mathbb{E}(x-x_o)
$$
$$
\mathbb{E}(f(x)) > \mathbb{E}(f(x_o)) + m (\,\mathbb{E}(x)-\mathbb{E}(x_o))
$$
Substituting $x$ as $X$ and $x_o$ as $\mathbb{E}(X)$ 
$$
\mathbb{E}(f(X)) > \mathbb{E}(f(\mathbb{E}(X))) + m (\,\mathbb{E}(X)-\mathbb{E}(\mathbb{E}(X)))
$$
> Expectation of X is a constant so Expectation of expectation of X is the same as Expectation of X

> Also E[x] is a constant so Expectation of $f(c)$ is the same as $f(c)$

Using the above two points
$$
\mathbb{E}[f(X)] > f(\mathbb{E}[X])
$$

Note still what is the condition for greater than equality , I'm not sure. 

Just how we have proved the condition for convex functions, we can do the same for concave functions by assuming that the entire functions lies below the tangent at any point. 