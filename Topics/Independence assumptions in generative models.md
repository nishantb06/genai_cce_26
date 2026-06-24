# Independence Assumptions and Joint Density Factorisation

This comes directly from the independence assumptions of the generative model. Let's go through it carefully.

---

## Step 1: The Prior over the Latent Variables

The paper states

$$z_n \overset{\text{iid}}{\sim} \mathcal{N}(0, I), \qquad n = 1, \dots, N.$$

The notation $\overset{\text{iid}}{\sim}$ means:

1. **Identically distributed:** every $z_n$ has the same distribution, $z_n \sim \mathcal{N}(0, I)$
2. **Independently distributed:** knowing one $z_i$ tells you nothing about any other $z_j$.

For independent random variables, the joint density factorizes:

$$p(z_1, \dots, z_N) = p(z_1), p(z_2) \cdots p(z_N) = \prod_{n=1}^N p(z_n).$$

Therefore,

$$p(\mathbf{z}) = \prod_n p(z_n).$$

There is nothing VAE-specific here — this is just the definition of independence.

---

## Step 2: The Likelihood

The model also states

$$x_n \mid z_n \sim \mathcal{N}(\mu(z_n; \theta),, \Sigma(z_n; \theta)).$$

This means:

1. Each observation $x_n$ depends only on its own latent variable $z_n$.
2. Given all latent variables $\mathbf{z}$, the observations are conditionally independent.

Graphically:

```
z1 → x1
z2 → x2
...
zN → xN
```

There are no arrows like:

```
z1 → x2
x1 → x2
```

So once you know $\mathbf{z}$, each $x_n$ is generated independently. Conditional independence gives

$$p_\theta(x_1, \dots, x_N \mid \mathbf{z}) = \prod_{n=1}^N p_\theta(x_n \mid \mathbf{z}).$$

But $x_n$ only depends on $z_n$, so

$$p_\theta(x_n \mid \mathbf{z}) = p_\theta(x_n \mid z_n).$$

Hence,

$$p_\theta(\mathbf{x} \mid \mathbf{z}) = \prod_{n=1}^N p_\theta(x_n \mid z_n).$$

---

## Step 3: Why Do Papers Make This Assumption?

Without these independence assumptions, you'd need to model

$$p(z_1, \dots, z_N)$$

and

$$p(x_1, \dots, x_N \mid z_1, \dots, z_N),$$

which could have arbitrary dependencies and become computationally intractable.

The VAE instead assumes the much simpler generative process:

1. Sample each latent independently: $z_n \sim \mathcal{N}(0, I)$
2. Generate each data point independently from its latent: $x_n \sim p_\theta(x_n \mid z_n)$

These assumptions are what allow the joint density to factorize:

$$p_\theta(\mathbf{x}, \mathbf{z}) = p(\mathbf{z}), p_\theta(\mathbf{x} \mid \mathbf{z}) = \left(\prod_n p(z_n)\right)\left(\prod_n p_\theta(x_n \mid z_n)\right) = \prod_n p(z_n), p_\theta(x_n \mid z_n).$$

This factorization is one of the main reasons VAEs are computationally manageable.