We are approximating the true distribution as a linear combination of M [[Gaussian Distributions]] all with different means and variances. 

## Example from Classical ML — Gaussian Mixture Model (GMM)

Let $z$ is discrete: $z \in {1, 2, \ldots, M}$

$$P_\theta(x) = \sum_z P_\theta(x, z) = \sum_z P_\theta(z) \cdot P_\theta(x \mid z)$$

$$P_\theta(x) = \sum_{j=1}^{M} P_\theta(z=j) \cdot P_\theta(x \mid z=j)$$

In a GMM:

$$P_\theta(z = j) = \alpha_j$$
$\alpha_j$ is now a scalar

**And now we assume that** the conditional probability of x given z is a gaussian distribution 
$$P_\theta(x \mid z = j) = \mathcal{N}(x;, \mu_j,, \Sigma_j)$$

Therefore the full GMM model is:

$$P_\theta(x) = \sum_{j=1}^{M} \alpha_j \cdot \mathcal{N}(x;, \mu_j,, \Sigma_j)$$

---

## Parameters of a GMM

The gaussian we mentioned above is a multivariate gaussian distribution where each [[Gaussian Distributions|gaussian]] has a mean vector and a covariance matrix

$$\theta = {\alpha_1, \alpha_2, \ldots, \alpha_M,; \mu_1, \mu_2, \ldots, \mu_M,; \Sigma_1, \Sigma_2, \ldots, \Sigma_M}$$

with constraints:

$$x \in \mathbb{R}^d, \quad \mu_j \in \mathbb{R}^d, \quad \Sigma_j \in \mathbb{R}^{d \times d}$$

$$0 \leq \alpha_j \leq 1, \quad \sum_{j=1}^{M} \alpha_j = 1$$

---

## Goal: Estimate $\theta$ via ELBO Optimisation

$$  
(\hat{\theta}, \hat{q}) = \arg\max_{\theta,\, q} J_{\theta}(q)  
$$

The above optimisation can be solved **iteratively** by optimising for $\theta$ and $q$ one after the other.

---

## Algorithm — [[Expectation Maximisation]] (EM)
Let $\theta_t$ and $q_t$ represent the estimates at iteration $t$.

**For** $t = 1$ **to** $T$:

**E-step** (fix $\theta^t$, optimise over $q$):

$$q_{t+1}^* = \arg\max_q ; J_{\theta^t}(q), \quad \text{with } \theta^t \text{ held constant}$$

**M-step** (fix $q_{t+1}$, optimise over $\theta$):

$$\theta_{t+1}^* = \arg\max_\theta ; J_\theta(q_{t+1}), \quad \text{with } q_{t+1} \text{ held constant}$$

> It can be shown that EM ensures the log-likelihood is non-decreasing: $$\ell(\theta_{t+1}) \geq \ell(\theta_t)$$

We iteratively alternate between the above two steps untill convergence, like [[K-means clustering]] , in fact we can show that K-means is a a special case of GMM's

---

## EM for GMM

### E-step

$$q_{t+1}^* = \arg\max_q ; J_\theta(q) = P_\theta(z \mid x)$$

> It can be analytically shown that the best $q^*(z \mid x)$ that optimises the ELBO is $P_\theta(z \mid x)$.

[[When we cant find the best value of the posterior of the latent varaible]]

Expanding via [[Bayes Rule]]:

$$q_{t+1}^* = P_{\theta_t}(z \mid x) = \frac{P_{\theta_t}(x \mid z) \cdot P_{\theta_t}(z)}{P_{\theta_t}(x)}, \quad P_{\theta_t}(x) = \sum_z P_{\theta_t}(x \mid z), P_{\theta_t}(z)$$

For the GMM specifically:

$$q_{t+1}^*(z=i \mid x) = \frac{\mathcal{N}(x\;, \mu_i^t,\, \Sigma_i^t)\, \alpha_i^t}{\sum_{j=1}^{M} \mathcal{N}(x\;, \mu_j^t,\, \Sigma_j^t)\, \alpha_j^t}$$

### M-step

$$\theta^{t+1} = \arg\max_\theta \; J_\theta(q_{t+1}^*)$$

Solved by differentiating $J_\theta(q_{t+1}^*)$ with respect to $\theta = (\alpha, \mu, \Sigma)$ and solving for $\theta$.

---

## Limitation of EM

The ELBO can be optimised for a latent variable model using the EM algorithm, **provided $P_\theta(z \mid x)$ can be computed**.

If $P_\theta(z \mid x)$ cannot be estimated for a given latent variable model, then **EM fails**.

> **Open Question:** How to learn a latent variable model for cases where $P_\theta(z \mid x)$ is unknown?
> **Answer** : [[VAEs]] are the first in the line of models that help answer this question. 

---

### Sampling from GMM / How is GMM a sampler
Lets say you have a six component GMM , you role a dice and as per the number which comes up , you choose that gaussian and then sample from it. 
Note the GMM is trained so we would have the mean vector and the covariance matrix for each multivariate Gaussian. Also choosing which which gaussians to choose from is not exactly uniform like a dice .As we are training the alphas as well.

--- 

## Code
```python
from sklearn.mixture import GaussianMixture
```

## Tags

#GMM #gaussian-mixture-model #EM-algorithm #expectation-maximisation #ELBO #latent-variable-models #clustering #machine-learning
