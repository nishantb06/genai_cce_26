## Deriving the Evidence Lower Bound (ELBO)

Recall from the previous section:

$$\ell(\theta) = \log\, \mathbb{E}_{q(z \mid x)}\left( \frac{P_\theta(x, z)}{q(z \mid x)} \right)$$

Applying Jensen's inequality (since $\log$ is concave):

$$\ell(\theta) \geq \mathbb{E}_{q(z \mid x)} \log \left( \frac{P_\theta(x, z)}{q(z \mid x)} \right) =: J_\theta(q)$$

Therefore:

$$\boxed{\ell(\theta) \geq J_\theta(q)}$$

where $\ell(\theta)$ is called the **[[Evidence]]** and $J_\theta(q)$ is called the **[[Evidence Lower Bound]] (ELBO)**.