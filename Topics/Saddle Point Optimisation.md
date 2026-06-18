## Definition

**Saddle point optimisation** (also called **min–max optimisation**) is an optimisation problem where we **minimise with respect to one set of parameters** and **maximise with respect to another**:

$$\min_{\theta} \max_{\omega}\; J(\theta, \omega)$$

At a saddle point $(\theta^*, \omega^*)$, $J$ is at a minimum along $\theta$ and a maximum along $\omega$ — neither player can improve unilaterally.

---

## Why It Is Difficult

Unlike standard minimisation, saddle point problems are **hard to train in practice**:

- **Saturation** — if the discriminator becomes too strong (or too weak), its output saturates (e.g. $D_\omega(x) \approx 0$ or $\approx 1$), and gradients vanish. The generator then receives little useful signal.
- **Instability** — alternating updates to $\theta$ and $\omega$ can oscillate rather than converge. Small imbalances between the two networks lead to mode collapse, divergence, or degraded sample quality.

The generator and discriminator must stay **roughly balanced** throughout training — a delicate equilibrium that makes adversarial learning notoriously fragile.

---

## Where It Appears

In generative modelling, the VDM objective

$$\theta^*, \omega^* = \arg\min_\theta \max_\omega \left[ \mathbb{E}_{P_x} T_\omega(x) - \mathbb{E}_{P_\theta} f^*\!\left(T_\omega(x)\right) \right]$$

is a saddle point problem. [[Generative Adversarial Networks (GANs)|GANs]] solve it by alternating gradient descent on $\theta$ (generator) with gradient ascent on $\omega$ (discriminator).

---

## Related

- [[Generative Adversarial Networks (GANs)]] — alternating min–max training in practice
- [[Interpretation of a GAN as a Classifier-Guided Generative Sampler]] — intuitive view of the two-player setup
- [[Realization of Variational Divergence Minimisation (VDM)]] — where the min–max objective is derived
- [[Generative Modelling]]

---

## Tags

#saddle-point #min-max-optimisation #adversarial-training #GAN #optimisation #machine-learning
