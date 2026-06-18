To minimise a [[F-Divergence]] between the data distribution and a model without evaluating the intractable integral directly, we need a tractable surrogate objective.

The starting point is [[Expressing distance metric in terms of expectations over density function|expressing the divergence metric as a variational lower bound]]: rewrite $D_f$ using the convex conjugate of $f$, lift the supremum outside the integral, and optimise over a restricted function class $\mathbb{T}$.
