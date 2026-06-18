The convex conjugate is brought into the [[Expressing distance metric in terms of expectations over density function|$D_f$ derivation]] because it turns an **intractable f-divergence integral** into a **tractable variational objective** built from **expectations**.

---

## The problem with the starting form

You start with:

$$D_f\left(P_x \,\|\, P_\theta\right) = \int_x p_\theta(x)\, f\!\left(\frac{p_x(x)}{p_\theta(x)}\right) \mathrm{d}x$$

This is awkward for training because:

1. **$p_x$ is unknown** — you only have samples, not the density.
2. **The ratio $p_x/p_\theta$ is inside $f$** — you cannot easily plug in samples.
3. **$p_\theta$ may also be implicit** (e.g. GANs) — you cannot evaluate the integrand pointwise.

So the goal is: **rewrite $D_f$ into something estimable from data and model samples.**

---

## Is $p_x/p_\theta$ convex?

**No.** The ratio $u(x) = p_x(x)/p_\theta(x)$ is not a convex function of $x$ in general — it is just a **positive scalar** (for each $x$ where both densities are positive) that we plug into $f$.

What **is** convex is the generator function **$f(u)$**, not the ratio itself. By definition of an [[F-Divergence|f-divergence]], $f : \mathbb{R}^+ \to \mathbb{R}$ is required to be convex (see [[Constraints on the choice of the f function]]). That convexity is what guarantees $D_f \geq 0$ via [[Jensen's inequality]], and it is also what makes the [[Convex conjugate function|convex conjugate]] $f^*$ well-defined and useful.

At each $x$, we evaluate $f$ at the **argument** $u = p_x(x)/p_\theta(x) \in \mathbb{R}^+$ — we are not claiming that the map $x \mapsto p_x(x)/p_\theta(x)$ is convex.

---

## What the conjugate does

For convex $f$, the Fenchel conjugate gives (see [[Convex conjugate function]]):

$$f(u) = \sup_t \left\{ tu - f^*(t) \right\}$$

That replaces the nonlinear $f(u)$ with a **supremum over a linear function** in $u$, plus a penalty $f^*(t)$.

Substitute $u = \dfrac{p_x(x)}{p_\theta(x)}$:

$$\int p_\theta(x)\, f\!\left(\frac{p_x}{p_\theta}\right) \mathrm{d}x
= \int p_\theta(x)\, \sup_t \left\{ t\frac{p_x}{p_\theta} - f^*(t) \right\} \mathrm{d}x$$

The key algebraic step — multiply $p_\theta$ into the linear term:

$$t\frac{p_x}{p_\theta} \cdot p_\theta = t\, p_x$$

So the integrand splits into terms involving **$p_x$ and $p_\theta$ separately**, not their ratio trapped inside $f$.

---

## Why that matters: expectations appear

After lifting $\sup_t$ to $\sup_{T(x)}$, you get:

$$\sup_{T} \int \left\{ T(x)\, p_x(x) - p_\theta(x)\, f^*(T(x)) \right\} \mathrm{d}x$$

which is:

$$\sup_{T}\; \mathbb{E}_{x \sim p_x}[T(x)] - \mathbb{E}_{x \sim p_\theta}[f^*(T(x))]$$

That is exactly what you wanted:

- first term → estimate from **data samples**
- second term → estimate from **model samples**
- $T(x)$ → parametrize with a neural net (discriminator / critic)

The conjugate is what makes this decomposition possible.

---

## Why conjugate, and not Jensen?

[[Jensen's inequality]] is used elsewhere (e.g. ELBO in [[Latent Variable Models]]) for **concave** functions like $\log$:

$$\log \mathbb{E}[\cdot] \geq \mathbb{E}[\log \cdot]$$

Here the structure is different: you have **$f(\text{ratio})$ inside an integral weighted by $p_\theta$**, and $f$ is **convex**, not concave. The conjugate is the standard rewrite for convex $f$:

| Tool | When it applies | What it gives |
|------|-----------------|---------------|
| Jensen | concave $g$, form $\log \mathbb{E}[\cdot]$ | lower bound on log-likelihood (ELBO) |
| Fenchel conjugate | convex $f$, form $f(u)$ | sup representation → variational $D_f$ objective |

---

## Why introduce $T(x)$ at all?

The pointwise $\sup_t$ at each $x$ is solved by some $t^*(x)$ — a **function of $x$**, not a single scalar. So you introduce $T : \mathcal{X} \to \mathbb{R}$ and optimize over a restricted class $\mathbb{T}$ (e.g. neural networks).

That gives:

- **Equality** if $\mathbb{T}$ contains the true optimizer $T^*$
- **Lower bound** if it does not — which is still useful as a training objective

That is the "variational" in [[Variational Divergence Minimization]].

---

## One-sentence summary

**We bring in the convex conjugate because it rewrites $f(p_x/p_\theta)$ as a supremum over an auxiliary function $T$, which turns the f-divergence into a difference of expectations under $p_x$ and $p_\theta$ — something you can actually optimize from samples.**

---

## Related

- [[Expressing distance metric in terms of expectations over density function]] — full derivation
- [[Convex conjugate function]] — definition and properties of $f^*$
- [[F-Divergence]] — where $f$ and $D_f$ are defined
- [[integrals in terms of expectations]] — estimating the resulting expectations from samples
- [[Variational Divergence Minimization]] — using the bound to train models

---

## Tags

#f-divergence #conjugate-function #variational-lower-bound #convex-analysis #generative-modelling #machine-learning
