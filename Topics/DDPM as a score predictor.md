Related to [[Score based models]]

Suppose $t \sim \mathcal{N}(t;, \mu_t, \Sigma_t) = p(t)$

**[[Tweedie's formula]]**

$$\mathbb{E}\left[\mu_t \mid t\right] = t + \Sigma_t \cdot \nabla_t \log p(t)$$

where $\nabla_t \log p(t)$ defined as the [[Score function]]

---

Recall, that in a DDPM,

$$q(x_t \mid x_0) = \mathcal{N}\!\left(x_t;\; \sqrt{\bar{\alpha}_t}\cdot x_0,\; (1-\bar{\alpha}_t)\, I\right)$$

Apply Tweedie's formula to above,

$$\mathbb{E}(\mu \mid x_t) = x_t + (1-\bar{\alpha}_t)\cdot \nabla_{x_t} \log p(x_t)$$

The best estimate for $\mathbb{E}(\mu \mid x_t)$ is the true mean. $\Rightarrow \mathbb{E}(\mu \mid x_t) = \sqrt{\bar{\alpha}_t}\cdot x_0$.

$$\sqrt{\bar{\alpha}_t}\cdot x_0 = x_t + (1-\bar{\alpha}_t)\cdot \nabla_{x_t} \log p(x_t)$$

Rearranging the terms,

$$\boxed{x_0 = \frac{x_t + (1-\bar{\alpha}_t)\cdot \nabla_{x_t} \log p(x_t)}{\sqrt{\bar{\alpha}_t}}}$$
#### Rewrite the Consistency Term in Terms of Score Functions
$$\mu_q(x_t, x_0) = \frac{\sqrt{\alpha_t},(1-\bar{\alpha}_{t-1})\cdot x_t + \sqrt{\bar{\alpha}_{t-1}},(1-\alpha_t)\cdot \overbrace{\dfrac{x_t + (1-\bar{\alpha}_t)\cdot \nabla_{x_t} \log p(x_t)}{\sqrt{\bar{\alpha}_t}}}^{x_0}}{1-\bar{\alpha}_t}$$

$$\boxed{\mu_q = \frac{1}{\sqrt{\alpha_t}}\cdot x_t + \frac{1-\alpha_t}{\sqrt{\alpha_t}}\cdot \nabla_{x_t} \log p(x_t)}$$

$$\mu_\theta = \frac{1}{\sqrt{\alpha_t}}\cdot x_t + \frac{1-\alpha_t}{\sqrt{\alpha_t}}\cdot S_\theta(x_t)$$

$S_\theta(x_t)$ : predicted score using NN.

Consistency term $\propto |\mu_q - \mu_\theta|_2^2$

$$\propto \left|\nabla_{x_t} \log p(x_t) - S_\theta(x_t)\right|_2^2$$

Regression over the Score function.

#### Diagram
NN predicts the score of the distribution

$$x_{t} , t \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \ \text{dim}};\theta;\substack{\text{increase} \ \text{dim}}} \rightarrow S_\theta(x_t) \qquad \left|\nabla_{x_t} \log p(x_t) - S_\theta(x_t)\right|_2^2$$

$\hookrightarrow$ Regressor on the score function

#### To Compute the True Score

$$x_0 = \frac{x_t + (1-\bar{\alpha}_t)\cdot \nabla_{x_t} \log p(x_t)}{\sqrt{\bar{\alpha}_t}} \quad -(1)$$

Also, $x_0 = \underbrace{\dfrac{x_t - \sqrt{1-\bar{\alpha}_t}\cdot \epsilon_t}{\sqrt{\bar{\alpha}_t}}}_{(2)}$ by definition, $\quad \epsilon_t \sim \mathcal{N}(0, I)$

Equating (1) & (2), & rearranging

$$\nabla_{x_t} \log p(x_t) = \frac{-1}{\sqrt{1-\bar{\alpha}_t}}\; \epsilon_t$$

True score $=$ negatively scaled noise

$\Rightarrow$ a DDPM trained to [[DDPM as a regression over added noise|regress over added noise]], is implicitly predicting the score function.

This is obvious because . Score should point to the direction that is opposite to that of the noise.