Closed-form [[KL-Divergence]] between two [[Gaussian Distributions]].

## Results

##### Univariate

Let $p = \mathcal{N}(\mu_1, \sigma_1^2)$ and $q = \mathcal{N}(\mu_2, \sigma_2^2)$.

$$\boxed{D_{\mathrm{KL}}(p \,\|\, q) = \log\!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{\sigma_1^2 + (\mu_1 - \mu_2)^2}{2\sigma_2^2} - \frac{1}{2}}$$

##### Multivariate

Let $p = \mathcal{N}(\mu_1, \Sigma_1)$ and $q = \mathcal{N}(\mu_2, \Sigma_2)$, with $x \in \mathbb{R}^d$.

$$\boxed{D_{\mathrm{KL}}(p \,\|\, q) = \frac{1}{2}\left[\log \frac{|\Sigma_2|}{|\Sigma_1|} - d + \mathrm{tr}\!\left(\Sigma_2^{-1}\Sigma_1\right) + (\mu_1 - \mu_2)^\top \Sigma_2^{-1}(\mu_1 - \mu_2)\right]}$$

The univariate formula is the $d=1$ special case with $\Sigma_i = \sigma_i^2$.

---

## Proof (univariate)

Start from the definition:

$$D_{\mathrm{KL}}(p \,\|\, q) = \int p(x)\, \log\!\left(\frac{p(x)}{q(x)}\right)\, dx$$

Write the two densities explicitly:

$$p(x) = \frac{1}{\sqrt{2\pi\sigma_1^2}} \exp\!\left(-\frac{1}{2}\left(\frac{x-\mu_1}{\sigma_1}\right)^2\right), \qquad q(x) = \frac{1}{\sqrt{2\pi\sigma_2^2}} \exp\!\left(-\frac{1}{2}\left(\frac{x-\mu_2}{\sigma_2}\right)^2\right)$$

The log-ratio simplifies to a constant plus a quadratic in $x$:

$$\log\!\left(\frac{p(x)}{q(x)}\right) = \log\!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{1}{2}\left[\frac{(x-\mu_2)^2}{\sigma_2^2} - \frac{(x-\mu_1)^2}{\sigma_1^2}\right]$$

So

$$D_{\mathrm{KL}}(p \,\|\, q) = \log\!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{1}{2}\,\mathbb{E}_p\!\left[\frac{(x-\mu_2)^2}{\sigma_2^2} - \frac{(x-\mu_1)^2}{\sigma_1^2}\right]$$

Three standard [[Moment|moments]] of $p$ finish the integral:

$$\int p(x)\, dx = 1, \qquad \int x\, p(x)\, dx = \mu_1, \qquad \int x^2\, p(x)\, dx = \mu_1^2 + \sigma_1^2$$

For the cross term,

$$\mathbb{E}_p[(x-\mu_2)^2] = \mathbb{E}_p[(x-\mu_1 + \mu_1 - \mu_2)^2] = \sigma_1^2 + (\mu_1 - \mu_2)^2$$

and $\mathbb{E}_p[(x-\mu_1)^2] = \sigma_1^2$. Substituting,

$$D_{\mathrm{KL}}(p \,\|\, q) = \log\!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{1}{2}\left[\frac{\sigma_1^2 + (\mu_1 - \mu_2)^2}{\sigma_2^2} - 1\right]$$

which is the boxed univariate result.

The multivariate proof is the same idea: expand $\log(p/q)$, then use $\mathbb{E}_p[x]=\mu_1$, $\mathbb{E}_p[(x-\mu_1)(x-\mu_1)^\top]=\Sigma_1$, and matrix trace identities.

---

## Special case: $q = \mathcal{N}(0, 1)$

Set $\mu_2 = 0$, $\sigma_2 = 1$:

$$D_{\mathrm{KL}}(p \,\|\, q) = -\log \sigma_1 + \frac{\sigma_1^2 + \mu_1^2}{2} - \frac{1}{2} = \frac{1}{2}\left(\mu_1^2 + \sigma_1^2 - 1 - \log \sigma_1^2\right)$$

Equivalently (common in [[VAEs]]),

$$\boxed{D_{\mathrm{KL}}(\mathcal{N}(\mu, \sigma^2) \,\|\, \mathcal{N}(0,1)) = \frac{1}{2}\left(\mu^2 + \sigma^2 - 1 - \log \sigma^2\right)}$$

##### Diagonal multivariate case

If $p = \mathcal{N}(\mu, \mathrm{diag}(\sigma_1^2, \ldots, \sigma_d^2))$ and $q = \mathcal{N}(0, I)$ with independent dimensions,

$$D_{\mathrm{KL}}(p \,\|\, q) = \sum_{d=1}^{D} \frac{1}{2}\left(\mu_d^2 + \sigma_d^2 - 1 - \log \sigma_d^2\right)$$

This sum form applies only when the covariance matrix is diagonal (dimensions are independent).

---

## Handwritten notes

![[Pasted image 20260707160059.png]]
![[Pasted image 20260707160049.png]]

![[IMG_0777.jpeg]]
![[IMG_0776.jpeg]]
![[Pasted image 20260707155400.png]]
