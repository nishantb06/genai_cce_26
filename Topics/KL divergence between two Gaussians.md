##### For Univariate
$$\boxed{\log\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{\sigma_1^2 + (\mu_1 - \mu_2)^2}{2\sigma_2^2} - \frac{1}{2}}$$

##### For [[Multivariate Gaussian Distribution]] 
$$\boxed{\frac{1}{2}\left[\log \frac{|\Sigma_2|}{|\Sigma_1|} - d + \mathrm{tr}\!\left(\Sigma_2^{-1}\Sigma_1\right) + (\mu_1 - \mu_2)^T \Sigma_2^{-1}(\mu_2 - \mu_1)\right]}$$
### Proof
First we can take the prove for a univariate Gaussians. Then we can notice that the Results for Univariate and [[Multivariate Gaussian Distribution]] is very similar. 

The key thing to know is that the following three integrals will come when you put the formula for the Gaussian into the KL divergence integral. Those three integrals will be eliminated
$$
\int x.p(x)dx = \mu
$$
$$
\int p(x)dx = 1
$$
$$
\int x^2.p(x)dx = \mu^2 + \sigma^2
$$
The above is the second [[Moment]] and is a known result. 


# Gaussian for the Univariate

$$\mathcal{N}(x \mid \mu, \sigma^2) \triangleq \frac{1}{\sqrt{2\pi\sigma^2}}, e^{-\frac{1}{2\sigma^2}(x-\mu)^2}$$

$$= \frac{1}{\sqrt{2\pi},\sigma}, e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$

This is the gaussian for a univariate distribution.

---

$$D_f(p | q) = \int q(x), f!\left(\frac{p(x)}{q(x)}\right) dx$$

ratio based $f$ divergence

When $f(x) = x \log x$, i.e. $f(r) = r \log r$, for KL divergence.

$$D_f(p | q) = \int \cancel{q(x)} \cdot \frac{p(x)}{\cancel{q(x)}} \cdot \log!\left(\frac{p(x)}{q(x)}\right) dx$$

$$\text{KL divergence} = \int p(x) \cdot \log!\left(\frac{p(x)}{q(x)}\right) dx$$

---

Let

$$p(x) = \frac{1}{\sqrt{2\pi\sigma_1^2}}, e^{-\frac{1}{2}\left(\frac{x-\mu_1}{\sigma_1}\right)^2}$$

$$q(x) = \frac{1}{\sqrt{2\pi\sigma_2^2}}, e^{-\frac{1}{2}\left(\frac{x-\mu_2}{\sigma_2}\right)^2}$$

Substituting

$$KL = \int \frac{1}{\sqrt{2\pi\sigma_1^2}}, e^{-\frac{1}{2}\left(\frac{x-\mu_1}{\sigma_1}\right)^2} \cdot \log\left( \frac{\dfrac{1}{\sqrt{2\pi\sigma_1^2}}, e^{-\frac{1}{2}\left(\frac{x-\mu_1}{\sigma_1}\right)^2}}{\dfrac{1}{\sqrt{2\pi\sigma_2^2}}, e^{-\frac{1}{2}\left(\frac{x-\mu_2}{\sigma_2}\right)^2}} \right)$$

$$\underbrace{\hspace{2cm}}_{\text{constant}}$$

$$\frac{a^b}{a^c} = a^{b-c}$$

$$\log!\left(\frac{\sigma_2}{\sigma_1}, e^{\frac{1}{2}\left[\left(\frac{x-\mu_2}{\sigma_2}\right)^2 - \left(\frac{x-\mu_1}{\sigma_1}\right)^2\right]}\right)$$

$$\log!\left(\frac{\sigma_2}{\sigma_1}\right) \cdot e^{\frac{1}{2}\left[\left(\frac{x-\mu_2}{\sigma_2} + \frac{x-\mu_1}{\sigma_1}\right)\left(\frac{x-\mu_2}{\sigma_2} - \frac{x-\mu_1}{\sigma_1}\right)\right]}$$

$$\log!\left(\frac{\sigma_2}{\sigma_1}\right) \qquad \left(\frac{\sigma_1 x - \mu_2\sigma_1 + \sigma_2 x - \mu_1\sigma_2}{\sigma_1\sigma_2}\right)$$

$$\cdot \left(\frac{(\sigma_1+\sigma_2)x - (\mu_2\sigma_1 + \mu_1\sigma_2)}{\sigma_1\sigma_2}\right)$$

$$\left(\frac{(\sigma_1-\sigma_2)x + (\mu_1\sigma_2 - \mu_2\sigma_1)}{\sigma_1\sigma_2}\right)$$

$$e^{\frac{1}{2(\sigma_1\sigma_2)^2}\left[(\sigma_1+\sigma_2)x - (\mu_2\sigma_1 + \mu_1\sigma_2)\right]\left[(\sigma_1-\sigma_2)x + (\mu_1\sigma_2 - \mu_2\sigma_1)\right]}$$

$$(\sigma_1^2 - \sigma_2^2)x^2 + x\left[(\sigma_1+\sigma_2)(\mu_1\sigma_2 - \mu_2\sigma_1) - (\sigma_1-\sigma_2)(\mu_2\sigma_1 + \mu_1\sigma_2)\right]$$

$$x\left[\mu_1\sigma_1\sigma_2 - \mu_2\sigma_1^2 + \mu_1\sigma_2^2 - \cancel{\mu_2\sigma_1\sigma_2} - \mu_1\sigma_1^2 - \cancel{\mu_1\sigma_1\sigma_2} + \cancel{\mu_2\sigma_1\sigma_2} + \mu_1\sigma_2^2\right]$$

$$2x\left[\mu_1\sigma_2^2 - \mu_2\sigma_1^2\right]$$
$$(\sigma_1^2 - \sigma_2^2)x^2 + 2x(\mu_1\sigma_2^2 - \mu_2\sigma_1^2)$$

$$- \underbrace{(\mu_2\sigma_1 + \mu_1\sigma_2)}_{b}\underbrace{(\mu_1\sigma_2 - \mu_2\sigma_1)}_{a-b}$$

$$- (\mu_1^2\sigma_2^2 - \mu_2^2\sigma_1^2)$$

$$= (\sigma_1^2 - \sigma_2^2)x^2 + 2x(\mu_1\sigma_2^2 - \mu_2\sigma_1^2) + (\mu_2^2\sigma_1^2 + \mu_1^2\sigma_2^2)$$

$$\int \frac{1}{\sqrt{2\pi\sigma_1^2}}\cdot e^{-\frac{1}{2}\left(\frac{x-\mu_1}{\sigma_1}\right)^2} \left[\log!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{[\cdots]}{2\sigma_1^2\sigma_2^2}\right]$$

$$\int p(x) \left[\log!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{(\sigma_1^2-\sigma_2^2)x^2 + 2x(\mu_1\sigma_2^2 - \mu_2\sigma_1^2) + (\cdots)}{2,\sigma_1^2\sigma_2^2}\right]$$

---

$$\int \log!\left(\frac{\sigma_2}{\sigma_1}\right)\cdot p(x),dx = \log\frac{\sigma_2}{\sigma_1} \underbrace{\int p(x),dx}_{\rightarrow 1}$$

$$\left(\frac{\sigma_1^2-\sigma_2^2}{\sigma_1^2\sigma_2^2}\right)\int x^2\cdot p(x),dx = \frac{(\sigma_1^2-\sigma_2^2)(\mu_1^2 + \sigma_1^2)}{2,(\sigma_1^2\sigma_2^2)} \quad \rightarrow (\mu_1^2 + \sigma_1^2)$$

$$\int x\cdot p(x),dx = \frac{2(\mu_1\sigma_2^2 - \mu_2\sigma_1^2),\mu_1}{2,\sigma_1^2\sigma_2^2} \quad \rightarrow \mu_1$$

$$3^{\text{rd}} = \frac{\mu_2^2\sigma_1^2 - \mu_1^2\sigma_2^2}{2,\sigma_1^2\sigma_2^2}$$
$$\log!\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{(\sigma_1^2 - \sigma_2^2)(\mu_1^2 + \sigma_1^2)}{(\sigma_1^2\sigma_2^2)}$$

$$+ \frac{(\mu_1\sigma_2^2 - \mu_2\sigma_1^2),\mu_1}{\sigma_1^2\sigma_2^2} = \frac{2\mu_1^2\sigma_2^2 - 2\mu_1\mu_2\sigma_1^2}{\sigma_1^2\sigma_2^2}$$

$$+ \frac{\mu_2^2\sigma_1^2 - \mu_1^2\sigma_2^2}{\sigma_1^2\sigma_2^2}$$

$$= \frac{\mu_1^2\sigma_1^2 - \cancel{\mu_1^2\sigma_2^2} + \sigma_1^4 - \sigma_1^2\sigma_2^2 + \cancel{\mu_1^2\sigma_2^2} - \mu_1\mu_2\sigma_1^2 + \mu_2^2\sigma_1^2 - \cancel{\mu_1^2\sigma_2^2}}{\sigma_1^2,\sigma_2^2}$$

$$\frac{\sigma_1^4 - \sigma_1^2\sigma_2^2 + \mu_1^2\sigma_1^2 - \cancel{2\mu_1^2\sigma_2^2} + \mu_2^2\sigma_1^2 - \mu_1\mu_2\sigma_1^2}{2\sigma_1^2\sigma_2^2}$$

$$\frac{\sigma_1^4 - \sigma_1^2\sigma_2^2 + \mu_1^2\sigma_1^2 + \mu_2\sigma_1^2 - 2\mu_1\mu_2\sigma_1^2}{2\sigma_1^2\sigma_2^2}$$

$$= \frac{\sigma_1^2 - \sigma_2^2 + (\mu_1 - \mu_2)^2}{2\sigma_2^2}$$
$$\boxed{\log\left(\frac{\sigma_2}{\sigma_1}\right) + \frac{\sigma_1^2 + (\mu_1 - \mu_2)^2}{2\sigma_2^2} - \frac{1}{2}}$$

If $\sigma_2 = 1$, $\mu_2 = 0$ i.e $q(x) = \mathcal{N}(0,1)$

$$-\log\sigma_1 + \frac{\sigma_1^2}{2} + \frac{\mu_1^2}{2} - \frac{1}{2}$$

$$\frac{-1}{2}\left(1 + \log\sigma^2 - \sigma_1^2 - \mu_2^2\right)$$

$$= \frac{-1}{2}\left[1 + \log(\sigma^2) - (\mu^2 + \sigma^2)\right]$$

---

For $D$ dimensions:

$$KL\left(p(x) ,|, \mathcal{N}(0,1)\right) = \sum_{d=1}^{D} \frac{1 + \log(\sigma_d^2) - (\mu_d^2 + \sigma_d^2)}{\ }$$

$\hookrightarrow$ but only if the dimensions are independent

i.e the covariance matrix is (has) only diagonal entries

---
Photos of handwritten notes
![[Pasted image 20260707160059.png]]
![[Pasted image 20260707160049.png]]

![[IMG_0777.jpeg]]
![[IMG_0776.jpeg]]
![[Pasted image 20260707155400.png]]