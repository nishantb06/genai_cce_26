## Data Generation or Sampling

> Encoder is not used here

Consider the following sampling procedure:

We know that
$$p_\theta(x) = \int_z p_\theta(x, z), \mathrm{d}z$$

**i)** Sample a $z_\text{new} \sim p(z) = \left[\mathcal{N}(0, I)\right]$

**ii)** Sample a $x_\text{new} \sim p_\theta(x|z)$, using Decoder of the VAE.

> $z \sim q_\phi(z|x)$  
> $z_\text{new} \sim \mathcal{N}(0, I)$  
> $p_\theta(x|z) \rightarrow \hat{x}_\theta(z) = \text{mean of } p_\theta(x|z)$  
> Dec

We don't the latent prior but The KL term in ELBO will ensure that

$$q_\phi(z|x) = p(z) = \mathcal{N}(0, I) \quad \forall, x$$

If the VAE is well trained, $q_\phi(z|x) = \mathcal{N}(0, I)\ \forall x$  
$\Rightarrow$ sampling from $\mathcal{N}(0, I)$ $\Rightarrow$ sampling from $q_\phi(z|x)$

---

$\hat{x}_\theta(z_\text{new})$ is the output of Decoder for $z_\text{new} \sim \mathcal{N}(0, I)$

Either

**i)** use $\hat{x}_\theta(z_\text{new})$ as the novel generated datapoint, $\hat{x}_\theta(z_\text{new}) \in \mathbb{R}^d$

**ii)** $x_\text{new} \sim \mathcal{N}\!\left(\hat{x}_\theta(z_\text{new}),\, I\right)$ : novel generated data point.

$$\therefore\quad p_\theta(x|z) = \mathcal{N}\!\left(\hat{x}_\theta(z),\, I\right)$$
Because we had modelled the data posterior as a Gaussian distribution with Identity variance. 

---

## b) VAEs for Latent Posterior Inference or Embedding or Feature Extraction

> Decoders are not used

Consider the trained Encoder of a VAE.

$$x_\text{test} \rightarrow \underbrace{q_{\phi^*}(z|x)}_{\text{Encoder}} \rightarrow \mu_\phi(x_\text{test})$$

$$\rightarrow \Sigma_\phi(x_\text{test}), \qquad Z_\text{test} \in \mathbb{R}^k$$

The Embedding or the feature vector for $x_\text{test}$ is given by,

**a)** $Z_\text{test} = \mu_\phi(x_\text{test})$ , Can take the embedding as the mean vector itself

**b)** $Z_\text{test} \sim \mathcal{N}\!\left(\mu_\phi(x_\text{test}),\, \Sigma_\phi(x_\text{test})\right)$ . Or you can sample an encoding from the Gaussian distribution that the latent posterior represents.


Read next : [[Posterior Collapse in naive VAE]]




