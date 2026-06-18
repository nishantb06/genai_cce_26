## Definition

If $f(u)$ is a convex function, its **convex conjugate** (Fenchel conjugate) $f^*(t)$ is defined as:

$$f^*(t) = \sup_{u \in \operatorname{dom} f} \left\{ ut - f(u) \right\}$$

where $\operatorname{dom} f = \{ u : f(u) < \infty \}$. Here for every t we need to solve an optimisation problem to get the conjugate of a convex function.

---

## Properties of the Convex Conjugate $f^*(t)$

**i)** $f^*(t)$ is convex (even if $f$ is not strictly convex).

**ii)** **Fenchel biconjugation:** Under mild regularity (e.g. $f$ is convex, proper, and lower semi-continuous), the conjugate of the conjugate recovers $f$:

$$\left[f^*\right]^* = f
\quad \Longrightarrow \quad
f(u) = \sup_{t \in \operatorname{dom} f^*} \left\{ tu - f^*(t) \right\}$$

This $\sup$ representation is what we use when rewriting [[F-Divergence|D_f]].

**iii)** **Fenchel–Young inequality:** For all $u \in \operatorname{dom} f$ and $t \in \operatorname{dom} f^*$:

$$f(u) + f^*(t) \geq ut$$

with equality iff $t \in \partial f(u)$ (i.e. $t$ is a subgradient of $f$ at $u$).

**iv)** **Domain:** $f^*$ is defined on the dual space of subgradients. In the f-divergence setting, $u = p_x/p_\theta > 0$, so we work with $f : \mathbb{R}^+ \to \mathbb{R}$ and choose $T(x) \in \operatorname{dom} f^*$.

**v)** **Examples:**

| $f(u)$ | $f^*(t)$ |
|--------|----------|
| $u \log u$ (KL) | $e^{t-1}$ |
| $\tfrac{1}{2}|u - 1|$ (TV) | piecewise quadratic on $[-\tfrac{1}{2}, \tfrac{1}{2}]$ |

---

## Related

- [[Convexity condition]] — definition of convexity for $f$
- [[Constraints on the choice of the f function]] — why $f$ must be convex in f-divergence
- [[Expressing distance metric in terms of expectations over density function]] — where the conjugate is applied
- [[Why convex conjugate in f-divergence]] — motivation for bringing in $f^*$

---

## Tags

#convex-analysis #conjugate-function #fenchel-conjugate #f-divergence #machine-learning
