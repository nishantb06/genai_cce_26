## Setup

$$\mathcal{D} = \left\{ x_1, x_2, \ldots, x_n \right\} \sim \text{iid } P_x$$

$$z \sim \mathcal{N}(0, I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim P_\theta(\hat{x}) \longrightarrow \boxed{D_\omega(x)} \longrightarrow [0, 1]$$

**Goal:** $P_\theta(\hat{x})$ to be close to $P_x(x)$.

This classifier-guided view motivates the adversarial min–max objective that [[Realization of Variational Divergence Minimisation (VDM)|VDM]] derives from an [[F-Divergence|f-divergence]] — see [[Generative Adversarial Networks (GANs)|GANs]] for the resulting training loss.

---

## The Discriminator as a Binary Classifier

Suppose there is a binary classifier:

$$D_\omega(x) = \begin{cases} 1 & \text{if } x \sim P_x \\ 0 & \text{if } x \sim P_\theta \end{cases}$$

$D_\omega(x)$ is a binary classifier between the samples of $P_x$ and $P_\theta$.

**Question:** Can $D_\omega(x)$ be used for making $P_\theta$ and $P_x$ closer?

**Answer:** Tweak $\theta$ (parameters of $g_\theta$) until the classifier 'fails' to distinguish between the samples of $P_x$ and $P_\theta$.

---

## Caveat — Classifier Failure $\not\Rightarrow$ $P_x = P_\theta$

However, failure of the classifier need not imply $P_x = P_\theta$.

**Counter Example:** Consider $x \in \mathbb{R}^2$, $x_i \in \left\{ x_i^1, x_i^2 \right\}$.

A linear classifier $D_{\omega_1}$ may fail to separate $P_x$ from $P_{\theta_3}$ even when $P_x \neq P_{\theta_3}$, because the decision boundary passes through both classes incorrectly.

$$P_x = P_\theta \implies \text{classifier fails}$$

$$\text{classifier failure} \not\Rightarrow P_x = P_\theta$$

> Hence, the classifier has to be **simultaneously tweaked along with the generator**.

---

## Formulation of the Classifier-Guided Sampler

Suppose $D_\omega : \mathcal{X} \to [0, 1]$.

Let $D_\omega(x)$ represent the **likelihood of the sample $x$ coming from $P_x$**.

### Discriminator Objective

**Part 1** — Maximise the log-likelihood of $x \sim P_x$ coming from $P_x$:

$$\omega^* = \arg\max_\omega \left[ \mathbb{E}_{x \sim P_x} \log D_\omega(x) \right]$$

**Part 2** — Maximise the likelihood of $\hat{x} \sim P_\theta$ _not_ coming from $P_x$:

$$\mathbb{E}_{\hat{x} \sim P_\theta} \log\!\left(1 - D_\omega(\hat{x})\right) \quad \text{: likelihood that } \hat{x} \notin P_x$$

$$\omega^* = \arg\max_\omega \left[ \mathbb{E}_{\hat{x} \sim P_\theta} \log\!\left(1 - D_\omega(\hat{x})\right) \right]$$

**Combined discriminator objective:**

$$\omega^* = \arg\max_\omega \left\{ \mathbb{E}_{x \sim P_x}\!\left(\log D_\omega(x)\right) + \mathbb{E}_{\hat{x} \sim P_\theta} \log\!\left[1 - D_\omega(\hat{x})\right] \right\}$$

$$= \arg\max_\omega J(\theta, \omega)$$

---

## Generator Objective

The objective for the generator $g_\theta(z)$ is such that the classifier has to 'fail'. Invert the optimisation for the classifier:

$$\theta^* = \arg\min_\theta J(\theta, \omega)$$

---

## Combined Adversarial Objective

$$\theta^*, \omega^* = \arg\min_\theta \max_\omega J(\theta, \omega)$$

> This is **adversarial optimisation** — the generator minimises while the discriminator maximises the same objective $J(\theta, \omega)$. This is a [[Saddle Point Optimisation|saddle point problem]], which is difficult to train stably. The same setup arises when a specific $f$ is substituted into [[Realization of Variational Divergence Minimisation (VDM)|VDM]].

---

## Related

- [[Generative Adversarial Networks (GANs)]] — full GAN objective and training algorithm
- [[Saddle Point Optimisation]] — why min–max training is unstable
- [[Realization of Variational Divergence Minimisation (VDM)]] — theoretical min–max derivation
- [[F-Divergence]] — divergence framework underlying VDM
- [[Generative Modelling]]

---

## Tags

#GAN #discriminator #generator #adversarial-optimisation #classifier-guided-sampler #binary-classifier #generative-modelling #machine-learning
