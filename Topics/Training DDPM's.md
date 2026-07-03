# Training of a [[Denoising Diffusion Probabilistic Models (DDPM) | DDPM]]

Given a data point $x_0$ from the true data dist.

Repeat until convergence : $T \approx 1000$, $\alpha_1 \ldots \alpha_T$ are fixed $[0, 1]$

-  **Step 1** : sample a $t \sim \text{uniform}\,[0, T]$ from the uniform distribution. 

To see the treatment done to only on datapoint , ignore the $m$ notation. 
What we do to one datapoint, needs to be done to a batch of $M$ datapoints as well.
$$x_t^m \sim \mathcal{N}\!\left(x_t;\ \sqrt{\bar{\alpha}_t}\, x_0,\ (1-\bar{\alpha}_t)\, I\right) \quad : \ q(x_t \mid x_0)$$

$$x_t^m = \sqrt{\bar{\alpha}_t}\, x_0 + \sqrt{1-\bar{\alpha}_t}\cdot \epsilon_t \qquad \epsilon_t \sim \mathcal{N}(0, I)$$

$$\theta^{k+1} \leftarrow \theta^k - \beta\, \nabla_\theta\, J_\theta(q)$$

where $\displaystyle J_\theta(q) = \sum_{m=1}^{M} \left\|\hat{x}_\theta(x_t^m) - x_0\right\|_2^2$

$$M \subset \{0, \ldots, T\}$$
From the loss the third term requires us to sum over all values of t from 2 to T. Instead of doing that we sample a random t and do this sampling for M times. Take M number of t's , sum the L2 term for those M t's and then take the back propagation for that batch. 

Question : Lets say we sample 32 images from the dataset, each image will have a different t or the same one ? Or lets say M is 16 . then will each image have each of the 16 t's which will lead to an aggregate batch of 512 ?

As you can see there is no [[Saddle Point Optimisation]] problem . Its very elegant. We just have to pick a sample from the input data, sample a time step from a uniform distribution, and compute the t-th noisy latent vector corresponding to that by the recursive expression that we calculated before. 

---

## Diagram

$$x_t,\, t \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \\ \text{dim}}\;\theta\;\substack{\text{increase} \\ \text{dim}}} \rightarrow \hat{x}_\theta(x_t) \xrightarrow{\text{forward pass to compute } \hat{x}_\theta(x_t)} \nabla_\theta \sum_{m=1}^{M} \left\|\hat{x}_\theta(x_t^m) - x_0\right\|_2^2$$

Backward pass for Grad descent.

---
