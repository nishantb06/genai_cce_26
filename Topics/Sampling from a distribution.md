### Uniform Sampler (Base Distribution)

$$Z \sim \mathcal{U}[0, 1], \quad p_Z(z) = \begin{cases} 1 & 0 \leq z \leq 1 \\ 0 & \text{otherwise} \end{cases}$$

Random number generators (`rand`) are samplers from the uniform distribution.

### Transformation of Random Variables

If $Z \sim p_Z$ and $g_\theta(z)$ is a (differentiable) function, then $X = g_\theta(Z)$ has a distribution $P_X$ that depends on $g_\theta$.

$$\mathcal{U} : Uniform\,\,distribution$$
$$\mathcal{N} : Normal\,\,  distribution$$
**Example:**

$$Z \sim \mathcal{U}[0,1], \quad X = \sqrt{-2\log Z} \cdot \cos(2\pi Z) \implies P_X = \mathcal{N}(0, 1)$$

> The sampler for $P_\theta$ can be controlled by choosing $g_\theta(z)$.


So the summary is that we can sample easily from a uniform distribution through code. All random number generators do that. Then after we sample z from a uniform distribution, we use that [[Conversion function]] to get the corresponding x that is now sampled from a Gaussian Distribution