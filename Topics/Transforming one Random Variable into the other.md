# Transforming One Random Variable into Another

If

$$\varepsilon \sim \mathcal{N}(0, 1)$$

and you define

$$z = \mu + \sigma \varepsilon$$

then $z$ is also Gaussian:

$$z \sim \mathcal{N}(\mu, \sigma^2)$$

This follows from a general property:

> An affine transformation of a Gaussian random variable is also Gaussian.

---

## General Result

If

$$X \sim \mathcal{N}(m, s^2)$$

and

$$Y = aX + b$$

then

$$Y \sim \mathcal{N}(am + b, a^2 s^2)$$

---

## VAE Case

For the [[Reparameterization Trick]] in [[VAEs]]:

- $a = \sigma$
- $b = \mu$
- $m = 0$
- $s^2 = 1$

So

$$\mathbb{E}[z] = \mu + \sigma \, \mathbb{E}[\varepsilon] = \mu$$

and

$$\mathrm{Var}(z) = \sigma^2 \, \mathrm{Var}(\varepsilon) = \sigma^2$$

Therefore

$$z = \mu + \sigma \varepsilon \sim \mathcal{N}(\mu, \sigma^2)$$

---

## Multivariate Case

In the multivariate VAE setting, the same idea becomes

$$\varepsilon \sim \mathcal{N}(0, I), \qquad z = \mu + \Sigma^{1/2} \varepsilon$$

which implies

$$z \sim \mathcal{N}(\mu, \Sigma)$$

Most VAEs assume a diagonal covariance, so we write

$$z = \mu + \sigma \odot \varepsilon$$

where $\odot$ is element-wise multiplication and

$$z \sim \mathcal{N}\left(\mu, \operatorname{diag}(\sigma^2)\right)$$

---

## Why This Matters

This is precisely the [[Reparameterization Trick]]: instead of sampling directly from $\mathcal{N}(\mu, \Sigma)$, you sample noise from a fixed standard Gaussian and deterministically transform it into a sample from the desired Gaussian distribution.

The transform $z = g(\varepsilon)$ is differentiable in $\mu$ and $\sigma$, so gradients can flow back through the encoder.



---
Proof linked to the [[Reparameterization Trick]]

# The Change-of-Variables Identity in the Reparameterization Trick

That line is essentially a statement of the change-of-variables formula for probability densities. Let's unpack it carefully.

---

## Step 1: We Start with a Simple Random Variable

Suppose you have

$$\epsilon \sim p(\epsilon)$$

and define

$$z = g_\phi(\epsilon, x).$$

Here:

- $x$ is fixed (the observed datapoint),
- $\epsilon$ is the only source of randomness,
- $g_\phi$ is deterministic.

Because $z$ is obtained by deterministically transforming $\epsilon$, the distribution of $z$ is completely induced by the distribution of $\epsilon$.

---

## Step 2: Probability Mass Must Be Preserved

Consider a tiny interval around $\epsilon$:

$$[\epsilon,, \epsilon + d\epsilon].$$

The probability of landing inside this interval is approximately

$$p(\epsilon), d\epsilon.$$

Under the transformation $z = g_\phi(\epsilon, x)$, this interval maps to another tiny interval

$$[z,, z + dz].$$

Since the mapping is deterministic, these two intervals correspond to exactly the same event. Therefore their probabilities must be equal:

$$q_\phi(z|x), dz = p(\epsilon), d\epsilon.$$

This is exactly the statement in the paper.

---

## Step 3: In Multiple Dimensions

If

$$\epsilon \in \mathbb{R}^d, \qquad z \in \mathbb{R}^d,$$

then infinitesimal lengths become infinitesimal volumes:

$$d\mathbf{z} = \prod_i dz_i, \qquad d\boldsymbol{\epsilon} = \prod_i d\epsilon_i.$$

Probability conservation becomes

$$q_\phi(\mathbf{z}|x), d\mathbf{z} = p(\boldsymbol{\epsilon}), d\boldsymbol{\epsilon}.$$

This is what the paper writes as

$$q_\phi(\mathbf{z}|x) \prod_i dz_i = p(\boldsymbol{\epsilon}) \prod_i d\epsilon_i.$$

---

## Step 4: Where Is the Jacobian?

You may be wondering: shouldn't there be a Jacobian determinant somewhere?

Yes. The full change-of-variables formula is

$$q_\phi(\mathbf{z}|x) = p(\boldsymbol{\epsilon}) \left| \det \frac{\partial \boldsymbol{\epsilon}}{\partial \mathbf{z}} \right|.$$

Equivalently,

$$d\mathbf{z} = \left| \det \frac{\partial \mathbf{z}}{\partial \boldsymbol{\epsilon}} \right| d\boldsymbol{\epsilon}.$$

Multiplying these together gives

$$q_\phi(\mathbf{z}|x), d\mathbf{z} = p(\boldsymbol{\epsilon}), d\boldsymbol{\epsilon},$$

so the Jacobian factors cancel. The paper skips writing them explicitly and directly writes the probability-volume equality.

---

## Step 5: Why This Matters for VAEs

For a VAE we choose

$$\epsilon \sim \mathcal{N}(0, I),$$

and define

$$z = \mu_\phi(x) + \sigma_\phi(x) \odot \epsilon.$$

The randomness now comes entirely from $\epsilon$, whose distribution does not depend on $\phi$. Therefore,

$$\mathbb{E}_{q_\phi(z|x)}[f(z)] = \mathbb{E}_{p(\epsilon)}!\left[ f!\left( \mu_\phi(x) + \sigma_\phi(x) \odot \epsilon \right) \right].$$

The expectation is now over a fixed distribution $p(\epsilon)$, and $\phi$ appears only inside a deterministic function. This allows gradients to pass through $g_\phi$ using ordinary backpropagation.

---

The entire reparameterization trick rests on this probability-conservation identity:

$$\boxed{ q_\phi(\mathbf{z}|x), d\mathbf{z} = p(\boldsymbol{\epsilon}), d\boldsymbol{\epsilon} }$$

which is simply the multidimensional change-of-variables theorem applied to the deterministic mapping

$$\mathbf{z} = g_\phi(\boldsymbol{\epsilon}, x).$$
