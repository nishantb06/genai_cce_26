https://www.cs.columbia.edu/~blei/fogm/2020F/readings/HoffmanJohnson2016.pdf


We're interested in variational [[Expectation Maximisation]] (EM) in models of the form

$$p_\theta(\boldsymbol{x}) = \int p_\theta(\boldsymbol{x} \mid \boldsymbol{z}), p(\boldsymbol{z}), d\boldsymbol{z}, \tag{1}$$

where $p(\boldsymbol{z})$ is a prior on latent variables $\boldsymbol{z} = {z_n}_{n=1}^N$ and $p_\theta(\boldsymbol{x} \mid \boldsymbol{z})$ is a likelihood on observations $\boldsymbol{x} = {x_n}_{n=1}^N$ parameterized by $\theta$. In particular, we focus on variational auto-encoders (VAEs, also known as DLGMs) [1, 2], in which the prior and likelihood follow from the generative model

$$z_n \overset{\text{iid}}{\sim} \mathcal{N}(0, I), \qquad x_n \mid z_n \sim \mathcal{N}(\mu(z_n; \theta),, \Sigma(z_n; \theta)), \qquad n = 1, 2, \ldots, N, \tag{2}$$

where the mean $\mu(z_n; \theta)$ and the covariance $\Sigma(z_n; \theta)$ depend on the latent variable $z_n$ through a neural network with parameters $\theta$. We write joint densities as products of independent densities,

$$p(\boldsymbol{z}) = \prod_n p(z_n), \qquad p_\theta(\boldsymbol{x} \mid \boldsymbol{z}) = \prod_n p_\theta(x_n \mid z_n). \tag{3}$$

Proof of the above is present [[Independence assumptions in generative models | here]]

The model is fit by maximising the log evidence lower-bound (ELBO) $\mathcal{L}$,

$$\log p_\theta(\boldsymbol{x}) = \log \int p_\theta(\boldsymbol{x}, \boldsymbol{z}), d\boldsymbol{z} = \log \int q_\phi(\boldsymbol{z} \mid \boldsymbol{x}) \frac{p_\theta(\boldsymbol{x}, \boldsymbol{z})}{q_\phi(\boldsymbol{z} \mid \boldsymbol{x})}, d\boldsymbol{z} \geq \mathbb{E}_{q_\phi(\boldsymbol{z} \mid \boldsymbol{x})} \log \frac{p_\theta(\boldsymbol{x}, \boldsymbol{z})}{q_\phi(\boldsymbol{z} \mid \boldsymbol{x})} \triangleq \mathcal{L}(\theta, \phi), \tag{4}$$

where each term in the variational density $q_\phi(\boldsymbol{z} \mid \boldsymbol{x}) = \prod_n q_\phi(z_n \mid x_n)$ is a Gaussian in which the mean $\mu(z_n; \phi)$ and covariance $\Sigma(z_n; \phi)$ depend on the observation $x_n$ through a neural network with parameters $\phi$. In these models, the variational distribution $q_\phi(z_n \mid x_n)$ acts as a stochastic "encoder" from an observation $x_n$ to a distribution on the latent variable $z_n$, and the likelihood $p_\theta(x_n \mid z_n)$ acts as a stochastic "decoder" from the latent variable $z_n$ to a distribution on the observation $x_n$.

There are several ways to rewrite the objective $\mathcal{L}(\theta, \phi)$, and each provides its own perspective.


# 1. Evidence minus the posterior KL
emphasizes that the lower bound becomes tighter as the variational distribution better approximates the posterior
Thus we can improve the ELBO by improving the model log evidence log pθ(x), through the prior p(z) or the likelihood pθ(x | z), or by improving the variational posterior approximation qφ(z | x).
# 2. Average negative energy plus entropy

where the log joint log pθ(z, x) is interpreted as the negative energy in a Boltzmann distribution. Since we choose (θ, φ) to maximize the ELBO, this version highlights that a good posterior approximation qφ(z | x) must assign most of its probability mass to regions of low energy (i.e. high joint probability density) while also maximizing the entropy of qφ(z | x). This perspective is useful in contrasting variational EM with a maximum a-posteriori (MAP) approach; while MAP need only find a single value of z that maximizes the joint density (even if it lies in a region with very low posterior mass), the entropy term in the ELBO prevents qφ(z | x) from collapsing to an atom.

# 3. Reconstruction loss minus KL to prior
For each observation index n, this version has a reconstruction term for the nth observation and a KL divergence from each encoding distribution to the prior. We can interpret this KL-divergence term as a regularizer that is minimized when qφ(zn | xn) = p(zn) for all z; this perspective has been used to explain the tendency of variational EM to “prune out” many of the latent dimensions in z <=> [[Importance Weighted auto encoders  | IWAE]]

Then the paper goes on to rewrite the KL term in terms of the [[average encoding distribution]] and maybe that relates to [[VQ-VAE]]




