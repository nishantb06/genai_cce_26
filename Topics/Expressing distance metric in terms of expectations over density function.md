## Starting Point

$$D_f\left(P_x \,\|\, P_\theta\right) = \int_x p_\theta(x)\, f\!\left(\frac{p_x(x)}{p_\theta(x)}\right) \mathrm{d}x$$

The integral above is hard to optimise directly. We rewrite $f\!\left(p_x/p_\theta\right)$ using the [[Convex conjugate function|convex conjugate]] of $f$ — see [[Why convex conjugate in f-divergence]] for why this step is necessary and what problem it solves.

---

## Substituting into $D_f$

Let $u = \dfrac{p_x(x)}{p_\theta(x)}$. Then:

$$D_f\left(P_x \,\|\, P_\theta\right) = \int_x p_\theta(x)\, f(u)\, \mathrm{d}x$$

Using the conjugate representation $f(u) = \sup_t \left\{ tu - f^*(t) \right\}$ from [[Convex conjugate function]]:

$$= \int_x p_\theta(x) \sup_t \left\{ tu - f^*(t) \right\} \mathrm{d}x$$

$$= \int_x p_\theta(x) \sup_t \left\{ t \cdot \frac{p_x(x)}{p_\theta(x)} - f^*(t) \right\} \mathrm{d}x$$

---

## Lifting the Supremum Outside the Integral

Since the inner optimisation depends on $x$, its solution is a function of $x$. Define:

$$T : \mathcal{X} \to \operatorname{dom} f^*$$

where $T(x) \in \mathbb{T}$ is the space of functions containing solutions for the inner optimisation problem.

Lifting the $\sup$ outside the integral (the inner $\sup_t$ becomes $\sup_{T(x) \in \mathbb{T}}$):

$$D_f\left(P_x \,\|\, P_\theta\right) = \sup_{T(x) \in \mathbb{T}} \int_x p_\theta(x) \left\{ T(x) \frac{p_x(x)}{p_\theta(x)} - f^*(T(x)) \right\} \mathrm{d}x$$

---

## Variational Lower Bound on $D_f$

Since the function space $\mathbb{T}$ we optimise over **may not contain** the optimal $T^*(x)$ (the true solution to the inner optimisation), we get a lower bound:

$$D_f\left(P_x \,\|\, P_\theta\right) \geq \sup_{T(x) \in \mathbb{T}} \int_x p_\theta(x) \left\{ T(x) \frac{p_x(x)}{p_\theta(x)} - f^*(T(x)) \right\} \mathrm{d}x$$

> The space of functions $\mathbb{T}$ that we are optimising over may not contain the optimal $T^*(x)$, which is the solution for the inner optimisation — hence the inequality becomes a lower bound rather than an equality.

---

## Related

- [[Why convex conjugate in f-divergence]] — motivation for the conjugate rewrite
- [[Convex conjugate function]] — definition and properties of $f^*$
- [[F-Divergence]] — integral definition of $D_f$ that we start from
- [[integrals in terms of expectations]] — approximating the resulting expectation from samples
- [[Variational Divergence Minimization]] — using the variational bound to train generative models
- [[Generative Modelling]] — why we need a tractable divergence objective in the first place
- [[General Algo for solving ML]] — the training pipeline this derivation slots into

---

## Tags

#f-divergence #conjugate-function #variational-lower-bound #convex-analysis #generative-modelling #machine-learning
