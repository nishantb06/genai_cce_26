### Architecture

$$\underbrace{X}_{\text{data space}} \xrightarrow{\text{Enc}} \underbrace{Z}_{\text{latent space}} \xrightarrow{\text{Dec}} \hat{X}$$

where $\dim(Z) \ll \dim(X)$ (representations / embeddings).

---
## Setup

$$\mathcal{D} = {x_1, x_2, \ldots, x_n} \sim \text{iid } P_x$$

Suppose $P_\theta$ denotes a parametric model.

---

## Definition of a Latent Variable Model

$$P_\theta(x) = \sum_z P_\theta(x, z) \quad \text{(if } z \text{ is discrete)}$$

$$P_\theta(x) = \int_z P_\theta(x, z), dz \quad \text{(if } z \text{ is continuous)}$$

$Z$ is called the **Latent / Hidden / Unobserved** R.V.

> Typically, $z$ is jointly estimated along with the model parameters $\theta$.

For each $x_i \in \mathcal{D}$, we assume there exists a $z_i$ corresponding to each $x_i$.

---

## Cases

### a) Discrete Latent Variable — Clustering

$$z \in {1, 2, \ldots, M}, \quad x \in \mathbb{R}^d$$

For each $x_i \in \mathcal{D}$, $z_i \mid x_i$ represents the latent variable corresponding to $x_i$.

Since $z_i$ is discrete, each $x_i$ is clustered into one of $M$ categories — this is **Clustering**.

> Examples: **[[Gaussian Mixture Models]] (GMM)**, **K-Means Clustering**

---

### b) Continuous Latent Variable — Auto-Encoder

$$x \in \mathbb{R}^d, \quad z \in \mathbb{R}^k, \quad k \ll d$$

Here, $z_i \mid x_i$ represents a **feature vector** corresponding to the given $x_i$.

> Latent variable models can also be used as **generative models**.

---

## General Principle for Learning Latent Variable Models

Given data $\mathcal{D} = {x_i}_{i=1}^n \sim \text{iid } P_x$, let the latent variable model be:

$$P_\theta(x) = \int_z P_\theta(x, z), dz$$

**Goal:** Estimate the model parameters $\theta$, given $\mathcal{D}$.

### Derivation via [[KL-Divergence | KL Minimisation]]

$$\theta^* = \arg\min_\theta \left[ D_{\mathrm{KL}}\left(P_x | P_\theta\right) \right]$$

$$= \arg\min_\theta \left[ \int_x P_x(x) \log \frac{P_x(x)}{P_\theta(x)}, dx \right]$$

$$= \arg\min_\theta \left[ \int_x P_x(x) \log P_x(x), dx - \int_x P_x(x) \log P_\theta(x), dx \right]$$

The first term is **independent of $\theta$**, so:

$$= \arg\min_\theta \left[ -\int_x P_x(x) \log P_\theta(x), dx \right]$$

$$\boxed{\theta^* = \arg\max_\theta \left[ \mathbb{E}_{P_x} \log P_\theta(x) \right]} \quad \leftarrow \textbf{Maximum Likelihood Estimation (MLE)}$$

> $\log P_\theta(x)$ is the **log-likelihood function** of $P_\theta(x)$.

---

## Log-Likelihood in a Latent Variable Model

In a latent variable model, $P_\theta(x) = \int_z P_\theta(x, z), dz$, so the objective becomes:

$$\theta^* = \arg\max_\theta \left[ \mathbb{E}_{P_x} \log P_\theta(x) \right]$$

Let $\ell(\theta) = \log P_\theta(x)$. Then:

$$\ell(\theta) = \log P_\theta(x) = \log \int_z P_\theta(x, z), dz$$

---

## Introducing the Variational Distribution $q(z \mid x)$

Suppose $q(z \mid x)$ denotes a density function over the latent variable $z$, given $x$. Multiply and divide by $q(z \mid x)$ inside the integral:

$$\ell(\theta) = \log \int_z P_\theta(x, z), \frac{q(z \mid x)}{q(z \mid x)}, dz$$

$$= \log \int_z q(z \mid x) \left[ \frac{P_\theta(x, z)}{q(z \mid x)} \right] dz$$

Using the identity $\int_z q(z \mid x), g(z), dz = \mathbb{E}_{q(z \mid x)}[g(z)]$:

$$\ell(\theta) = \log \mathbb{E}_{q(z \mid x)}\left( \frac{P_\theta(x, z)}{q(z \mid x)} \right)$$

> This is the starting point for deriving the **Evidence Lower Bound (ELBO)**.

---

## [[Jensen's inequality]]

For any concave function (such as $\log$):

$$\log \mathbb{E}[\cdot] \geq \mathbb{E} \log[\cdot]$$

---

## Deriving the Evidence Lower Bound (ELBO)

> Log of sums is difficult to compute , sum of logs is easier to compute, which is why we invoke Jensens inequality to convert from one form to the other. This makes things slightly complex as we are now dealing with an inequality rather than an equality.

Recall from the previous section:

$$\ell(\theta) = \log\, \mathbb{E}_{q(z \mid x)}\left( \frac{P_\theta(x, z)}{q(z \mid x)} \right)$$

Applying Jensen's inequality (since $\log$ is concave):

$$\ell(\theta) \geq \mathbb{E}_{q(z \mid x)} \log \left( \frac{P_\theta(x, z)}{q(z \mid x)} \right) =: J_\theta(q)$$

Therefore:

$$\boxed{\ell(\theta) \geq J_\theta(q)}$$

where $\ell(\theta)$ is called the **[[Evidence]]** and $J_\theta(q)$ is called the **[[Evidence Lower Bound]] (ELBO)**.

---

## Interpretation

$J_\theta(q)$ is a function of both:

- the **model parameters** $\theta$, and
- the **density over $z$**, i.e. $q(z \mid x)$

> $q(z \mid x)$ is called the **Variational Latent Posterior**.

---

## Two Equivalent Objectives

**Original** maximum likelihood problem:

$$\theta^* = \arg\max_\theta\, \ell(\theta)$$

**Approximate** with ELBO:

$$\theta^* = \arg\max_{\theta,\, q}\; J_\theta(q)$$
> If we maximise the Lower Bound then in an indirect way we are automatically optimising for the the Evidence that is $\ell(\theta)$ . From here on onwards all models [[Variational Auto Encoders | VAE's]] , diffusion based models etc all work with this.  
---

## The Fundamental Problem in Latent Variable Generative Models

The core problem solved in _any_ latent variable generative model is **ELBO maximisation**:

> Find $\theta$ and $q$ that maximise the [[Evidence Lower Bound | ELBO]] $J_\theta(q)$.

$$\boxed{\theta^*, q^* = \arg\max_{\theta, q} \; \mathbb{E}_{q(z \mid x)} \log \frac{P_\theta(x, z)}{q(z \mid x)}}$$

---
Now that we have this example, a type of modelling (Classical ML) called [[Gaussian Mixture Models]] or GMM's comes into picture.
## Tags

#ELBO #evidence-lower-bound #Jensen-inequality #latent-variable-models #variational-inference #MLE #generative-modelling #machine-learning