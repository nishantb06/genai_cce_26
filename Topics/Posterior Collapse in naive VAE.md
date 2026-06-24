$$x \rightarrow q_\phi(z \mid x) \rightarrow z \rightarrow p_\theta(x \mid z) \rightarrow \hat{x}_\theta(z)$$

In a VAE, the second term in ELBO,

$$D_{\mathrm{KL}}\left(q_\phi(z \mid x) \,\|\, p(z)\right) \text{ is minimized}$$

$\forall x$, $q_\phi(z \mid x)$ is forcefully made to be the same as $p(z)$ $\left(\mathcal{N}(0, I)\right)$.

The decoder will see it difficult to differentiate b/w two input samples $x_i$ & $x_j$

Found this really good line in [[ELBO Surgery paper]]
> Ideally it would be small, but we do not want or expect it to approach 0, since that would imply that x and z were almost independent, whereas virtually all of our modelling power comes from strongly coupling x to z. So if the KL term is large, is that a sign of underfitting, overfitting, or neither?

$$\therefore \quad q_\phi(z \mid x_i) = q_\phi(z \mid x_j) = \mathcal{N}(0, I)$$

$$z_i \sim q_\phi(z \mid x_i) \qquad z_j \sim q_\phi(z \mid x_j)$$

---

### Solution for Posterior Collapse in VAE

$$J_\theta(q_\phi) = \underbrace{\|x - \hat{x}_\theta(z)\|_2^2}_{\text{reconstruction term on } x} + \underbrace{D_{\mathrm{KL}}\left(q_\phi(z \mid x) \,\|\, p(z)\right)}_{\text{Regularization term on } z}$$
[[Regularization]]

---

VAE can be viewed as an auto-Encoder with a regularized latent space (Regularized Auto-Encoder).

Typical regularized cost in ML looks like:

$$L_\theta(\cdot) + \lambda \cdot \Omega(\theta)$$

$$\underbrace{\hspace{1.5cm}}_{\text{Cost fn}} \qquad \underbrace{\hspace{1.5cm}}_{\substack{\text{regularization fn} \ \text{reg const} \rightarrow}}$$

In a VAE, viewed as regularized AE, the regularization constant is absent.

$\lambda$ will tradeoff between bias and variance

VAE can be made to trade-off b/w cost & regularization by adding a regularization constant to ELBO.

$$\hat{J}_\theta(q_\phi) = \|x - \hat{x}_\theta(z)\|_2^2 + \beta \, D_{\mathrm{KL}}\left[q_\phi(z \mid x) \,\|\, p(z)\right]$$

$$\beta\text{-VAE}, \quad 0 \leq \beta \leq 1, \quad \beta\text{ - hyper parameter}$$

- Higher $\beta$ $\rightarrow$ lead to posterior collapse, better generation
- Lower $\beta$ $\rightarrow$ reconstructions are better, generation will suffer $\quad q_\phi(z \mid x) \neq p(z)$

Here generation means that better variety amongst the samples ? For example on the MNIST dataset , with a higher Beta, different types of the number 4 are generated with higher beta ?

[[Training VAE's code]] also has $\beta$ more than 1 in [1,2,4,8] as well. 

Depending on the application whether you want better embeddings, perfect reconstruction or better generations, you can tweak the  [[Beta-VAE]]

Next reading [[VQ-VAE]]


