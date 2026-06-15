**Law of Large Numbers (WLLN):**

Given $\mathcal{D} = \{x_i\} \overset{\text{iid}}{\sim} p_X$, for any function $g$:
$$\frac{1}{N}\sum_{i=1}^{N} g(x_i) \xrightarrow[N \to \infty]{} \mathbb{E}[g(x)]$$
Now this can be computed with the help of code.