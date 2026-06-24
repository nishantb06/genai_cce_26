# Gradient Is a Linear Operator

A gradient is an operator that takes a function as input and returns its vector of partial derivatives.

For a scalar-valued function

$$f(x_1, x_2, \ldots, x_d)$$

the gradient is

$$\nabla f =
\begin{bmatrix}
\frac{\partial f}{\partial x_1} \\
\frac{\partial f}{\partial x_2} \\
\vdots \\
\frac{\partial f}{\partial x_d}
\end{bmatrix}$$

---

## What Linearity Means

An operator $L$ is called **linear** if it satisfies:

$$L(af + bg) = aL(f) + bL(g)$$

where $a$ and $b$ are constants.

Since the gradient is linear:

$$\nabla(af + bg) = a\nabla f + b\nabla g$$

So gradients distribute over addition and scalar multiplication.

---

## Basic Algebra Rules

### Sum Rule

$$\nabla_\psi \left[f_\psi(v) + g_\psi(v)\right]
= \nabla_\psi f_\psi(v) + \nabla_\psi g_\psi(v)$$

### Constant Multiple Rule

$$\nabla_\psi \left[c \cdot f_\psi(v)\right]
= c \cdot \nabla_\psi f_\psi(v)$$

where $c$ does not depend on $\psi$.

### Product Rule

The product rule is not linearity by itself, but it is used together with linearity:

$$\nabla_\psi \left[p_\psi(v) \cdot f_\psi(v)\right]
= \left(\nabla_\psi p_\psi(v)\right) f_\psi(v)
+ p_\psi(v) \left(\nabla_\psi f_\psi(v)\right)$$

---

## Why This Matters in VAEs

In [[VAEs]], we need to compute gradients of terms like:

$$\nabla_\psi \mathbb{E}_{P_\psi(v)} f_\psi(v)$$

Writing the expectation as an integral:

$$\nabla_\psi \mathbb{E}_{P_\psi(v)} f_\psi(v)
= \nabla_\psi \int_v p_\psi(v) f_\psi(v) \, \mathrm{d}v$$

Because the gradient is linear, under regularity assumptions we can move the gradient inside the integral:

$$= \int_v \nabla_\psi \left[p_\psi(v) f_\psi(v)\right] \, \mathrm{d}v$$

Then apply the product rule:

$$= \int_v \left(\nabla_\psi p_\psi(v)\right) f_\psi(v) \, \mathrm{d}v
+ \int_v p_\psi(v) \left(\nabla_\psi f_\psi(v)\right) \, \mathrm{d}v$$

Reordering the terms:

$$= \mathbb{E}_{P_\psi(v)} \nabla_\psi f_\psi(v)
+ \int_v \left(\nabla_\psi p_\psi(v)\right) f_\psi(v) \, \mathrm{d}v$$

The first term is an expectation and can be estimated by sampling.

The second term is harder because the gradient hits the probability density $p_\psi(v)$ itself.

This is the issue that motivates the [[Reparameterization Trick]].

---

## Intuition

Linearity says:

> The gradient of a sum is the sum of the gradients.

So when an objective has multiple pieces, like the VAE objective:

$$J_\theta(q_\phi)
= \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z)
- D_{\mathrm{KL}}\left(q_\phi(z \mid x) \,\|\, p_\theta(z)\right)$$

we can differentiate each part separately:

$$\nabla_\phi J_\theta(q_\phi)
= \nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z)
- \nabla_\phi D_{\mathrm{KL}}\left(q_\phi(z \mid x) \,\|\, p_\theta(z)\right)$$

The difficulty is not that gradients fail to distribute.

The difficulty is that $q_\phi(z \mid x)$ itself depends on $\phi$, so samples $z \sim q_\phi(z \mid x)$ also depend on $\phi$.

---

## Tags

#gradient #linearity #calculus #VAE #reparameterization-trick
