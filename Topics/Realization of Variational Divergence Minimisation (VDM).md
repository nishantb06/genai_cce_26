## Setup

Given data $\mathcal{D} = \{x_1, x_2, \ldots, x_n\} \sim \text{iid } P_x$:

$$z \sim \mathcal{N}(0, I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim P_\theta(\hat{x})$$

$$\theta^* = \arg\min_\theta D_f\left(P_x \,\|\, P_\theta\right)$$

---

## Variational Lower Bound on $D_f$

From the conjugate function derivation:

$$D_f\left(P_x \,\|\, P_\theta\right) \geq \max_{T(x) \in \mathbb{T}} \left[ \mathbb{E}_{P_x} T(x) - \mathbb{E}_{P_\theta} f^*\!\left(T(x)\right) \right]$$

---

## Approximating the Optimisation

The original objective:

$$\theta^* = \arg\min_\theta D_f\left(P_x \,\|\, P_\theta\right)$$

is approximated by minimising the lower bound instead:

$$\approx \arg\min_\theta \left[ \text{lower bound on } D_f \right]$$

$$= \arg\min_\theta \left[ \max_{T(x)} \left( \mathbb{E}_{P_x} T(x) - \mathbb{E}_{P_\theta} f^*\!\left(T(x)\right) \right) \right]$$

where the $\min$ is w.r.t. the parameters of $g_\theta(z)$, and the $\max$ is w.r.t. a class of functions $T(x) \in \mathbb{T}$.

---

## Parameterising $\mathbb{T}$ with a Neural Network

Represent $\mathbb{T}$ via a neural network $T_\omega(x)$, where $\omega$ are the parameters of the network. The objective becomes:

$$\theta^*, \omega^* = \arg\min_\theta \max_\omega \left[ \mathbb{E}_{P_x} T_\omega(x) - \mathbb{E}_{P_\theta} f^*\!\left(T_\omega(x)\right) \right]$$

---

## Implementing VDM for Generative Modelling

### Architecture

$$z \sim \mathcal{N}(0, I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim P_\theta(\hat{x}) \longrightarrow \boxed{T_\omega(x)} \longrightarrow T_\omega(x)$$

- $g_\theta(z)$ — **Generator Network**
- $T_\omega(x)$ — **Critic / Discriminator Network**

### Objective

$$J(\theta, \omega) = \mathbb{E}_{P_x} T_\omega(x) - \mathbb{E}_{P_\theta} f^*\!\left(T_\omega(x)\right)$$

$$\theta^*, \omega^* = \arg\min_\theta \max_\omega J(\theta, \omega)$$

> This is a **saddle point optimisation** — an **adversarial problem**.

---

## Output Activation of the Discriminator

The discriminator must satisfy $T_\omega(x) : \mathcal{X} \to \operatorname{dom} f^*$. This is enforced by composing a standard network output with an $f$-divergence-specific activation:

There is a fixed set of activation functions that must be used so the output of the generator maps cleanly to the input of the discriminator ![[images/Pasted image 20260618112849.png]]

$$T_\omega(x) = \sigma_f\!\left(V_\omega(x)\right)$$

where:

- $V_\omega(x) : \mathcal{X} \to \mathbb{R}$ — the linear (pre-activation) output of the network
- $\sigma_f(v) : \mathbb{R} \to \operatorname{dom} f^*$ — the **$f$-divergence-specific activation function**

### Network Pipeline

$$x \longrightarrow \boxed{V_\omega(x)} \xrightarrow{\mathbb{R}} \boxed{\sigma_f} \longrightarrow T_\omega(x) : \mathcal{X} \to \operatorname{dom} f^*$$

- $V_\omega(x)$ — linear layer
- $\sigma_f$ — $f$-divergence specific activation

---

## Final Objective (Expanded)

Substituting $T_\omega(x) = \sigma_f(V_\omega(x))$:

$$J(\theta, \omega) = \mathbb{E}_{P_x}\!\left[ \sigma_f\!\left(V_\omega(x)\right) \right] - \mathbb{E}_{P_\theta}\!\left[ f^*\!\left(\sigma_f\!\left(V_\omega(x)\right)\right) \right]$$

Choosing $f$ as in the [[F-Divergence|f-divergence]] for GANs and setting $D_\omega = \sigma_f \circ V_\omega$ recovers the standard [[Generative Adversarial Networks (GANs)|GAN]] loss — see also [[Interpretation of a GAN as a Classifier-Guided Generative Sampler]] for an intuitive reading of the discriminator.

---

## Tags

#VDM #variational-divergence-minimisation #GAN #generator #discriminator #saddle-point #adversarial #f-divergence #generative-modelling #machine-learning
