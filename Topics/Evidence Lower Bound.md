

## Deriving the Evidence Lower Bound (ELBO)

Recall from the previous section:

$$\ell(\theta) = \log\, \mathbb{E}_{q(z \mid x)}\left( \frac{P_\theta(x, z)}{q(z \mid x)} \right)$$

Applying [[Jensen's inequality]] (since $\log$ is concave):

$$\ell(\theta) \geq \mathbb{E}_{q(z \mid x)} \log \left( \frac{P_\theta(x, z)}{q(z \mid x)} \right) =: J_\theta(q)$$

Therefore:

$$\boxed{\ell(\theta) \geq J_\theta(q)}$$

where $\ell(\theta)$ is called the **[[Evidence]]** and $J_\theta(q)$ is called the **[[Evidence Lower Bound]] (ELBO)**.

ELBO can be optimised for a [[Latent Variable Models]] provided P_theta(z |x ) can be computed analytically. If we cant then that is the problem know [[Intractability]]

---
$$
\mathcal{L}(\theta, \phi)
=
\mathbb{E}_{z\sim q_\phi(z\mid x)}
\left[
\log \frac{p_\theta(x,z)}{q_\phi(z\mid x)}
\right]
\leq
\log p(x)
$$
---

# For [[VAEs]]
$$J_\theta(q_\phi) = \mathbb{E}_{q_\phi(z|x)} \log p_\theta(x|z) - D_{KL}\left[q_\phi(z|x) ,|, p(z)\right]$$
This is the equation for the ELBO