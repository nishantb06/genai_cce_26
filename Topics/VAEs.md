## Latent Variable Models

Given $\mathcal{D} = \left\{ x_i \right\}_{i=1}^n \sim \text{iid } P_x$, $x_i \in \mathbb{R}^d$

Lat. var. Model $p_\theta(x) = \int_z p_\theta(x, z) \, \mathrm{d}z$, $z \in \mathbb{R}^k$, $k \ll d$

$$\theta^* = \arg\min_\theta \left[ D_{\mathrm{KL}}\left(P_x \,\|\, P_\theta\right) \right]$$

$$= \arg\max_\theta \left[ \mathbb{E}_{P_x} \log p_\theta(x) \right] \quad \text{: Intractable}$$
Intractable because of the introduction of the latent variable model
So we resort to optimising the [[Evidence Lower Bound]]

Alternate problem using a lower bound on $\log p_\theta(x)$.

$$\theta^*, q^* = \arg\max_{\theta,\, q} J_\theta(q)$$

$$J_\theta(q) = \mathbb{E}_{q(z \mid x)} \log \frac{p_\theta(x, z)}{q(z \mid x)} \leq \log p_\theta(x)$$

---

## Goal of a Neural Latent Var Model

a) Learn a Lat. Var. Model with unknown $p_\theta(z \mid x)$. this is called the [[Intractability | Intractable]] [[Posterior distribution | Posterior]] in the paper [[AutoEncoding Variational Bayes]] i.e the OG VAE paper

b) Enable sampling / generation from $p_\theta(x \mid z)$.

c) Enable posterior Inference, compute / Estimate $q(z \mid x)$ called the Variational Approximation in the [[AutoEncoding Variational Bayes]] paper.

$\theta$ : Generative model params, $\phi$ : Variational params

# Algorithm for Neural Lat. Var. Model

$$p_\theta(x) = \int_z p_\theta(x, z) \, \mathrm{d}z$$

$$\theta^*, q^* = \arg\max_{\theta,\, q} J_\theta(q)$$

Consider $J_\theta(q) = \mathbb{E}_{q(z \mid x)} \log \dfrac{p_\theta(x, z)}{q(z \mid x)}$

$$= \mathbb{E}_{q(z \mid x)} \log \frac{p_\theta(x \mid z) \cdot p_\theta(z)}{q(z \mid x)}$$

$$= \mathbb{E}_{q(z \mid x)} \log p_\theta(x \mid z) - \mathbb{E}_{q(z \mid x)} \log \frac{q(z \mid x)}{p_\theta(z)}$$

$$J_\theta(q) = \mathbb{E}_{q(z \mid x)} \log p_\theta(x \mid z) - D_{\mathrm{KL}}\left(q(z \mid x) \,\|\, p_\theta(z)\right)$$

---

## To optimise $J_\theta(q)$ using Neural Networks

Represent $p_\theta(x \mid z)$ & $q(z \mid x)$ via Neural Networks.

$p_\theta(x \mid z)$ : conditional data likelihood

$q(z \mid x)$ : variational Latent posterior density

On a separate note 
In VAE's we use the Probabilistic way to interpret a neural network, read [[How to represent probability distributions via Neural Networks]] . NN gives the params of the distribution it is modelling. 


# VAE

Given $\mathcal{D} = \left\{ x_i \right\}_{i=1}^n \sim \text{iid } p_x$

$$p_\theta(x) = \int_z p_\theta(x, z) \, \mathrm{d}z \quad \text{: Model.}$$

The following objective is optimized.

$$J_\theta(q) = \mathbb{E}_{q(z \mid x)} \log p_\theta(x \mid z) - D_{\mathrm{KL}}\left(q(z \mid x) \,\|\, p_\theta(z)\right)$$

$q(z \mid x)$ & $p_\theta(x \mid z)$ are represented using prob. NNs.

Encoder: $x \longrightarrow \boxed{q_\phi(z \mid x)} \longrightarrow$ outputs params. of $q_\phi(z \mid x)$

Decoder: Samples using the above params $\longrightarrow \boxed{p_\theta(x \mid z)} \longrightarrow$ outputs params of $p_\theta(x \mid z)$

Sample $z \sim q_\phi(z \mid x)$ **This sampling operation happens outside of the Encoder/Decoder NN**

There is no direct connection b/w the Enc & Dec.

$\phi$ & $\theta$ denotes the weights of Enc & Dec, respectively.

$$\phi^*, \theta^* = \arg\max_{\theta,\, \phi} J_\theta(q_\phi)$$

$$\phi^{t+1} \leftarrow \phi^t + \alpha \, \nabla_\phi J_\theta(q_\phi)$$

$$\theta^{t+1} \leftarrow \theta^t + \alpha \, \nabla_\theta J_\theta(q_\phi)$$

Gradient descent to learn the Enc. & Dec.

Gradient Computation

$$J_\theta(q_\phi) = \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) - D_{\mathrm{KL}}\left(q_\phi(z \mid x) \,\|\, p_\theta(z)\right)$$

---

## To compute the gradients of $J_\theta(q_\phi)$ w.r.t. $\phi$

$$\nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z), \quad z \sim q_\phi(z \mid x)$$

The above term is similar to

$$\nabla_\psi \; \mathbb{E}_{P_\psi(v)} f_\psi(v)$$

where $P_\psi(v) = q_\phi(z \mid x)$, $f_\psi(v) = \log p_\theta(x \mid z)$, $v \to z$, $\psi \to \phi$.

$$\nabla_\psi \mathbb{E}_{P_\psi(v)} f_\psi(v) = \nabla_\psi \int_v P_\psi(v) \, f_\psi(v) \, \mathrm{d}v$$

[[Gradient is a Linear operator]] so we can push it inside the integral. 
$$= \int_v \nabla_\psi \left(p_\psi(v) \cdot f_\psi(v)\right) \mathrm{d}v$$
Using the [[Product rule]]
$$= \int_v \left(\nabla_\psi f_\psi(v)\right) \cdot p_\psi(v) \, \mathrm{d}v + \int_v \left(\nabla_\psi p_\psi(v)\right) f_\psi(v) \, \mathrm{d}v$$

$$= \mathbb{E}_{P_\psi(v)} \nabla_\psi f_\psi(v) + \underbrace{\int_v \left(\nabla_\psi p_\psi(v)\right) f_\psi(v) \, \mathrm{d}v}_{\text{is not an expectation} \;\therefore\; \text{can't be computed}}$$

$$\implies \nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) \quad \text{can't be computed}, \quad z \sim q_\phi(z \mid x)$$
Cant be computed because [[Integrals in terms of expectations]] cant be done here and hence cant be computed using [[Weak Law of Large Numbers | Sample averages]] 

There is one more problem which is that . [[Sampling is a non differentiable function]] 
Encoder -> Sampling -> Decoder. To compute the gradients / gradients to flow backwards the sampling procedure also has to be differentiable.

# The solution : [[Reparameterization Trick]]

