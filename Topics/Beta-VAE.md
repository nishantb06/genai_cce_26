Previous reading [[Posterior Collapse in naive VAE]]
$$\hat{J}_\theta(q_\phi) = \|x - \hat{x}_\theta(z)\|_2^2 + \beta \, D_{\mathrm{KL}}\left[q_\phi(z \mid x) \,\|\, p(z)\right]$$

$$\beta\text{-VAE}, \quad 0 \leq \beta \leq 1, \quad \beta\text{ - hyper parameter}$$
Next reading [[VQ-VAE]]
