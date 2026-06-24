Represent a RV in terms of another RV that is deterministic in nature
![[images/Pasted image 20260624120932.png]]

> **The variable wrt which we differentiate and the one wrt which we take the expectation should be different**

Recall, $\nabla_\psi \mathbb{E}_{P_\psi(v)} f_\psi(v)$ cannot be computed. $v \sim P_\psi(v)$.

Express the distribution $p_\psi(v)$ in terms of another distribution (another auxiliary RV) which is independent of the parameters $\psi$.

Suppose there exists an auxiliary RV, $\varepsilon \sim P_\varepsilon$. $P_\varepsilon$ is not dependent on $\psi$.

$$v = g(\varepsilon), \quad \text{then,}$$

$$\mathbb{E}_{P_\psi(v)} f_\psi(v) = \mathbb{E}_{P_\varepsilon} f_\psi\left(g(\varepsilon)\right) \quad \text{: Law of the Unconscious Statistician.}$$
This came using the [[Law of the Unconscious Statistician (LOTUS)]] 
$$\nabla_\psi \mathbb{E}_{P_\psi(v)} f_\psi(v) = \nabla_\psi \mathbb{E}_{P_\varepsilon} f_\psi\left(g(\varepsilon)\right)$$
iff there exists a function which transforms one RV into the other. 

$$\approx \frac{1}{M} \sum_{j=1}^{M} \nabla_\psi \left[ f_\psi\left(g(\varepsilon_j)\right) \right] \quad \varepsilon_j \sim P_\varepsilon, \quad \varepsilon_1, \ldots, \varepsilon_M \sim P_\varepsilon$$


What is happening here is that although the gradients are wrt $\psi$ here , the Expectation is not wrt $\psi$  . 

**So what flows back to the encoder is the average of gradients ?** 

---

# Examples of Reparameterization :

## a) $q_\phi(z \mid x) = \mathcal{N}\left(\mu_\phi(x),\, \Sigma_\phi(x)\right)$

Cited in [[AutoEncoding Variational Bayes]]
Latent posterior is a gaussian distribution.

$x \longrightarrow \boxed{q_\phi(z \mid x)} \longrightarrow \begin{cases} \mu_\phi(x),\, \Sigma_\phi(x) \end{cases}$ parameters of $q_\phi(z \mid x)$ for a given input $x$.

For every different x we have a different Latent posterior. We assume the posterior is a gaussian whose mean and sigma are coming from the encoder. 

Let $\varepsilon \sim \mathcal{N}(0, I)$, then 

$$z = \mu_\phi(x) + \Sigma_\phi(x) \cdot \varepsilon = g(\varepsilon) \quad \left(\mu + \Sigma\varepsilon\right)$$
The above is an element wise multiplication. 
Also refer to [[Transforming one Random Variable into the other]]
$$z \sim \mathcal{N}\left(\mu_\phi(x),\, \Sigma_\phi(x)\right)$$

---

## b) Inverse CDF Method.

Suppose $z$ is a RV & $F_z(z)$ denotes its CDF.

$$z = F_z^{-1}(\varepsilon), \quad \varepsilon \sim \mathcal{U}[0, 1]$$

$$g(\varepsilon) = F_z^{-1} \quad \text{(Inverse CDF),} \quad \varepsilon \sim \text{uniform } [0, 1]$$

---

Next read [[Training VAE's]]


---

From the paper
# Reparameterization Trick

This reparameterization is useful for our case since it can be used to rewrite an expectation w.r.t $q_\phi(\mathbf{z}|\mathbf{x})$ such that the Monte Carlo estimate of the expectation is differentiable w.r.t. $\phi$. A proof is as follows. Given the deterministic mapping $\mathbf{z} = g_\phi(\boldsymbol{\epsilon}, \mathbf{x})$ we know that $q_\phi(\mathbf{z}|\mathbf{x}) \prod_i dz_i = p(\boldsymbol{\epsilon}) \prod_i d\epsilon_i$. 
The above line comes from the proof of the [[Transforming one Random Variable into the other | Change of variables]] formula
Therefore$^1$,

$$\int q_\phi(\mathbf{z}|\mathbf{x}) f(\mathbf{z}), d\mathbf{z} = \int p(\boldsymbol{\epsilon}) f(\mathbf{z}), d\boldsymbol{\epsilon} = \int p(\boldsymbol{\epsilon}) f(g_\phi(\boldsymbol{\epsilon}, \mathbf{x})), d\boldsymbol{\epsilon}$$

It follows that a differentiable estimator can be constructed:

$$\int q_\phi(\mathbf{z}|\mathbf{x}) f(\mathbf{z}), d\mathbf{z} \simeq \frac{1}{L} \sum_{l=1}^{L} f(g_\phi(\mathbf{x}, \boldsymbol{\epsilon}^{(l)}))$$

where $\boldsymbol{\epsilon}^{(l)} \sim p(\boldsymbol{\epsilon})$. In section 2.3 we applied this trick to obtain a differentiable estimator of the variational lower bound.

---

$^1$ Note that for infinitesimals we use the notational convention $d\mathbf{z} = \prod_i dz_i$

