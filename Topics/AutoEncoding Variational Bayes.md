The original VAE Paper : https://arxiv.org/pdf/1312.6114

> How can we perform efficient approximate inference and learning with directed probabilistic models whose continuous latent variables and/or parameters have intractable posterior distributions?

This is the original question which lead to the creation of VAE's . [[Intractability]] means something that is difficult to solve. Here the latent posterior is difficult to solve . With [[Gaussian Mixture Models | GMM's]] we took the assumption that the latent posterior is a Gaussian and therefore we were able to solve it analytically. But in the general case we cant make that assumption.
If the ELBO or the Marginal distribution was intractable we would have used the [[Expectation Maximisation | EM algorithm]]


In addition to this the paper also introduces the [[Reparameterization Trick]] to make the [[Evidence Lower Bound | ELBO]] differentiable.

We are interested in, and propose a solution to, three related problems in the above scenario:
1. Efficient approximate ML or MAP estimation for the parameters θ. The parameters can be of interest themselves, e.g. if we are analyzing some natural process. They also allow us to mimic the hidden random process and generate artificial data that resembles the real data. 
2. Efficient approximate posterior inference of the latent variable z given an observed value x for a choice of parameters θ. This is useful for coding or data representation tasks. 
3. Efficient approximate marginal inference of the variable x. This allows us to perform all kinds of inference tasks where a prior over x is required. Common applications in computer vision include image denoising, inpainting and super-resolution.

# Reparameterization Trick

This reparameterization is useful for our case since it can be used to rewrite an expectation w.r.t $q_\phi(\mathbf{z}|\mathbf{x})$ such that the Monte Carlo estimate of the expectation is differentiable w.r.t. $\phi$. A proof is as follows. Given the deterministic mapping $\mathbf{z} = g_\phi(\boldsymbol{\epsilon}, \mathbf{x})$ we know that $q_\phi(\mathbf{z}|\mathbf{x}) \prod_i dz_i = p(\boldsymbol{\epsilon}) \prod_i d\epsilon_i$. 

For the proof of the above line read [[Transforming one Random Variable into the other]] last section.

Therefore$^1$,

$$\int q_\phi(\mathbf{z}|\mathbf{x}) f(\mathbf{z}), d\mathbf{z} = \int p(\boldsymbol{\epsilon}) f(\mathbf{z}), d\boldsymbol{\epsilon} = \int p(\boldsymbol{\epsilon}) f(g_\phi(\boldsymbol{\epsilon}, \mathbf{x})), d\boldsymbol{\epsilon}$$

It follows that a differentiable estimator can be constructed:

$$\int q_\phi(\mathbf{z}|\mathbf{x}) f(\mathbf{z}), d\mathbf{z} \simeq \frac{1}{L} \sum_{l=1}^{L} f(g_\phi(\mathbf{x}, \boldsymbol{\epsilon}^{(l)}))$$

where $\boldsymbol{\epsilon}^{(l)} \sim p(\boldsymbol{\epsilon})$. In section 2.3 we applied this trick to obtain a differentiable estimator of the variational lower bound.

---

$^1$ Note that for infinitesimals we use the notational convention $d\mathbf{z} = \prod_i dz_i$
