To minimise a [[F-Divergence]] between the data distribution and a model without evaluating the intractable integral directly, we need a tractable surrogate objective.

The starting point is [[Expressing distance metric in terms of expectations over density function|expressing the divergence metric as a variational lower bound]]: rewrite $D_f$ using the convex conjugate of $f$, lift the supremum outside the integral, and optimise over a restricted function class $\mathbb{T}$.

To turn this bound into a trainable algorithm, parameterise $T(x)$ with a neural network and alternate $\min_\theta$ / $\max_\omega$ — see [[Realization of Variational Divergence Minimisation (VDM)|how VDM is realised in practice]].

### Optimisation Reformulation

$$\theta^*, \omega^* = \arg\min_\theta \arg\max_\omega D(P_X \| P_\theta)$$

- In **GANs**: $g_\theta : Z \to X$ (generator maps latent $z$ to data $x$)
- In **VAEs / Latent Variable Models**: $X \leftrightarrow Z$ (encoder–decoder)
