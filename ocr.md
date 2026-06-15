

## 8. Variational Divergence Minimisation

### Optimisation Reformulation

$$\theta^*, \omega^* = \arg\min_\theta \arg\max_\omega D(P_X \| P_\theta)$$

- In **GANs**: $g_\theta : Z \to X$ (generator maps latent $z$ to data $x$)
- In **VAEs / Latent Variable Models**: $X \leftrightarrow Z$ (encoder–decoder)

---

## 10. Latent Variable Models

### Architecture

$$\underbrace{X}_{\text{data space}} \xrightarrow{\text{Enc}} \underbrace{Z}_{\text{latent space}} \xrightarrow{\text{Dec}} \hat{X}$$

where $\dim(Z) \ll \dim(X)$ (representations / embeddings).



### Discrete Latent Variable: Clustering

If $Z$ is discrete, $z \in \{1, 2, \ldots, M\}$:
- Each data point $x_i$ is assigned one of $M$ cluster values.
- Algorithms: **K-Means**, **GMM clustering**.

### Gaussian Distribution (Multivariate)

$$\mathcal{N}(x;\, \mu, \Sigma) = \frac{1}{(2\pi)^{d/2}|\Sigma|^{1/2}} \exp\!\left(-\frac{1}{2}(x-\mu)^\top \Sigma^{-1}(x-\mu)\right)$$

where $x \in \mathbb{R}^d$, $\mu \in \mathbb{R}^d$, $\Sigma \in \mathbb{R}^{d \times d}$.

### After Training a Latent Variable Model

Two uses:

1. **Embedding extraction (Clustering):**
   $$\text{Given } x_i, \text{ estimate } p_\theta(z \mid x_i) \quad \text{(encoder)}$$

2. **Generate new samples:**
   $$z_j \sim p(z),\quad z \in \{1, \ldots, M\} \implies x_i \sim \mathcal{N}(\mu_j, \Sigma)$$
   $$\implies \text{approximate } p_\theta(x)$$

---

## Tags

#generative-modelling #probability #machine-learning #VAE #GAN #latent-variable #MLE #KL-divergence #statistics