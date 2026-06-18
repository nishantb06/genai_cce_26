## Setup 

Given a dataset $\mathcal{D} = \{x_1, x_2, x_3, \ldots, x_n\}$ sampled [[Independent and Identically Distributed|iid]] from $P_x$ (unknown).

**Goal:** Estimate $P_x$ and learn to [[Sampling from a distribution|sample]] from it.

---

## General Principle of Generative Models

**i)** Assume a parametric family on $P_x$, denoted by $P_\theta$.

> $P_\theta$ is represented using Deep Neural Networks (the Model).

**ii)** Define and estimate a [[F-Divergence|divergence (distance) metric ]] between $P_\theta$ and $P_x$.

**iii)** Solve an optimisation problem over the parameters of $P_\theta$, to minimise the above divergence metric.

---

## Example

There is a R.V. $z \in \mathbb{R}^K$ with some arbitrary but known distribution:

$$z \sim \mathcal{N}(0, I)$$

Suppose $g_\theta(z) : \mathcal{Z} \to \mathcal{X}$, then:

$$\hat{x} = g_\theta(z)$$

has a different distribution than that of $z$, and the distribution of $\hat{x}$ depends on the function $g_\theta(\cdot)$.

Suppose $g_\theta(z)$ is a Neural Network. Denote the density of $\hat{x} = g_\theta(z)$ using $P_\theta(\hat{x})$.

$$z \sim \mathcal{N}(0,I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim P_\theta(\hat{x})$$

$$\theta^* = \arg\min_{\theta} D\!\left(P_x \,\middle|\, P_\theta\right)$$

Suppose $D(P_x \mid P_\theta)$ denotes a divergence measure between $P_x$ and $P_\theta$, with:

- $D \geq 0$
- $D = 0 \iff P_x = P_\theta$

---

## Optimisation Problem

$$\theta^* = \arg\min_{\theta} D\!\left(P_x \,\middle|\, P_\theta\right)$$

Upon solving the above optimisation problem, the distribution $P_x$ is **implicitly estimated** by $g_\theta(z)$, and one can sample from $P_x$ using $g_\theta(z)$:

$$z \sim \mathcal{N}(0,I) \longrightarrow \boxed{g_{\theta^*}(z)} \longrightarrow \hat{x} \sim P_{\theta^*}(\hat{x}) \quad (\text{close to } P_x)$$

A sample from $z \sim \mathcal{N}(0, I)$, passed through $g_{\theta^*}(z)$, produces a sample from $P_{\theta^*}(\hat{x})$ which is close to $P_x$ — so we end up sampling from $P_x$.

---

## The Open Questions

**i)** How to compute the divergence metrics without knowing $P_x$ and $P_\theta$? One route is to [[Expressing distance metric in terms of expectations over density function|re-express the divergence as an expectation]] that can be estimated from samples.

**ii)** What should be the choice of the divergence metric? answer : [[Constraints on the choice of the f function]]

**iii)** How to choose $g_\theta(z)$, and in turn $P_\theta$?

**iv)** How to solve the optimisation problem of minimising the divergence metric? [[Realization of Variational Divergence Minimisation (VDM)|Realise the variational bound]] with neural networks $g_\theta$ and $T_\omega$ in a min–max saddle-point problem.

---

## Tags

#generative-modelling #divergence #optimisation #neural-networks #sampling #machine-learning