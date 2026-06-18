## f-Divergence for GANs

GAN training minimises a particular [[F-Divergence|f-divergence]] between $P_x$ and $P_\theta$. For the original GAN, $f$ is chosen as follows (closely related to the [[Jenson Shannon Divergence | JS-divergence]]):

$$f(u) = u \log u - (u+1) \log(u+1)$$

$$f^*(t) = -\log\!\left(1 - \exp(t)\right), \quad \operatorname{dom} f^* = \mathbb{R}^-$$

$$\sigma_f(v) = -\log\!\left(1 + e^{-v}\right)$$

---

## GAN Objective from VDM

Substituting this $f$ into the general [[Realization of Variational Divergence Minimisation (VDM)|VDM objective]] $J(\theta, \omega)$:

$$J(\theta, \omega) = \mathbb{E}_{P_x}\!\left[ \sigma_f\!\left(V_\omega(x)\right) \right] - \mathbb{E}_{P_\theta}\!\left[ f^*\!\left(\sigma_f\!\left(V_\omega(x)\right)\right) \right]$$

Defining the **discriminator output** as the sigmoid function:

$$D_\omega(x) = \frac{1}{1 + e^{-V_\omega(x)}} \in [0, 1]$$

the objective simplifies to:

$$J_{\mathrm{GAN}}(\theta, \omega) = \mathbb{E}_{P_x}\!\left[ \log D_\omega(x) \right] + \mathbb{E}_{P_\theta}\!\left[ \log\!\left(1 - D_\omega(\hat{x})\right) \right]$$

---

## GAN Architecture

$$z \sim \mathcal{N}(0, I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim P_\theta(\hat{x}) \longrightarrow \boxed{D_\omega(x)} \longrightarrow [0, 1]$$

- $g_\theta(z)$ — **Generator Network** (MLP, FNN, CNN)
- $D_\omega(x)$ — **Discriminator / Binary Classifier** (CNN, MLP), output in $[0,1]$

The discriminator pipeline:

$$x \longrightarrow \boxed{V_\omega(x)} \xrightarrow{v \in \mathbb{R}} \boxed{\dfrac{1}{1+e^{-v}}} \longrightarrow D_\omega(x) \in [0,1]$$

---

## Implementation of GAN in Practice

**Input:** $\mathcal{D} = \left\{ x_1, x_2, x_3, \ldots, x_n \right\} \sim \text{iid } P_x$

The full objective approximated via mini-batches:

$$J_{\mathrm{GAN}}(\theta, \omega) = \frac{1}{B_1} \sum_{i=1}^{B_1} \log D_\omega(x_i) + \frac{1}{B_2} \sum_{j=1}^{B_2} \log\!\left(1 - D_\omega\!\left(g_\theta(z_j)\right)\right)$$

where:

$$x_1, \ldots, x_{B_1} \sim P_x$$

$$\hat{x}_1, \ldots, \hat{x}_{B_2} \sim P_\theta, \quad \hat{x}_j = g_\theta(z_j)$$

---

## Training Algorithm

### Training the Discriminator (keep $\theta$ constant)

**Steps:**

1. Sample a mini-batch $B_1 = \left\{ x_1, x_2, \ldots, x_{B_1} \right\} \subset \mathcal{D} \sim P_x$
2. Sample $z_1, z_2, \ldots, z_{B_2} \sim \mathcal{N}(0, I)$
3. Pass $z_1, \ldots, z_{B_2}$ through $g_\theta(\cdot)$ with fixed $\theta$ to get fake samples (forward + backward prop.)

**Discriminator objective** ($\omega$ update, $\theta$ fixed):

$$\omega^* = \arg\max_\omega \left[ \frac{1}{B_1} \sum_{i=1}^{B_1} \log D_\omega(x_i) + \frac{1}{B_2} \sum_{j=1}^{B_2} \log\!\left(1 - D_\omega\!\left(g_\theta(z_j)\right)\right) \right]$$

**Update rule** (one gradient ascent step):

$$\omega^{t+1} \leftarrow \omega^t + \alpha_1 \nabla_\omega J_{\mathrm{GAN}}(\theta, \omega)$$

> $\alpha_1$ is the step size. $\theta$ is kept constant.

---

### Training the Generator (keep $\omega$ constant)

The first term $\frac{1}{B_1}\sum \log D_\omega(x_i)$ is **independent of $\theta$**, so:

**Generator objective** ($\theta$ update, $\omega$ fixed):

$$\theta^* = \arg\min_\theta \left[ \frac{1}{B_2} \sum_{j=1}^{B_2} \log\!\left(1 - D_\omega\!\left(g_\theta(z_j)\right)\right) \right]$$

**Steps:**

1. Sample $z_1, \ldots, z_{B_2} \sim \mathcal{N}(0, I)$
2. Pass through $g_\theta(\cdot)$ then through $D_\omega(\cdot)$ with fixed $\omega$
3. Compute $\nabla_\theta J_{\mathrm{GAN}}$ and update $\theta$

**Update rule** (one gradient descent step):

$$\theta^{t+1} \leftarrow \theta^t - \alpha_2 \nabla_\theta J_{\mathrm{GAN}}(\theta, \omega)$$

> $\alpha_2$ is the step size. $\omega$ is kept constant.

---

## Summary: Training VDM / GAN

|Step|Network Updated|Other Network|Update Rule|
|---|---|---|---|
|Discriminator step|$\omega$|$\theta$ fixed|$\omega^{t+1} \leftarrow \omega^t + \alpha_1 \nabla_\omega J_{\mathrm{GAN}}$|
|Generator step|$\theta$|$\omega$ fixed|$\theta^{t+1} \leftarrow \theta^t - \alpha_2 \nabla_\theta J_{\mathrm{GAN}}$|

This alternating saddle-point optimisation is the **adversarial training** procedure at the heart of GANs.

---

## Related

- [[Realization of Variational Divergence Minimisation (VDM)]] — general min–max objective this note specialises
- [[F-Divergence]] — framework for choosing $f$ and $f^*$
- [[Interpretation of a GAN as a Classifier-Guided Generative Sampler]] — intuitive reading of the discriminator
- [[Variational Divergence Minimization]]
- [[Generative Modelling]]

---

## Tags

#GAN #generative-adversarial-network #VDM #discriminator #generator #adversarial-training #f-divergence #JSD #machine-learning #generative-modelling
