
Recall, the forward process of DDPM,

$$x_t = \sqrt{\bar{\alpha}_t}\cdot x_0 + \sqrt{1-\bar{\alpha}_t}\cdot \epsilon_t \qquad \epsilon_t \sim \mathcal{N}(0, I)$$

Rearranging the above terms,

$$x_0 = \frac{x_t - \sqrt{1-\bar{\alpha}_t}\cdot \epsilon_t}{\sqrt{\bar{\alpha}_t}} \quad -(1)$$

$\epsilon_t$ : noise added to $x_0$, to convert it into $x_t$.

Consistency term in the ELBO : $|\mu_\theta - \mu_q|_2^2$

- $\mu_q$ : mean of $q(x_{t-1} \mid x_t, x_0)$
- $\mu_\theta$ : mean of $p_\theta(x_{t-1} \mid x_t)$

Can we represent the consistency term in terms of the noise that is added ?
To do that :-
Represent $\mu_q$, in terms of $x_t$ & $\epsilon_t$.

$$\mu_q(x_t, x_0) = \frac{\sqrt{\alpha_t}\,(1-\bar{\alpha}_{t-1})\cdot x_t + \sqrt{\bar{\alpha}_{t-1}}\,(1-\alpha_t)\cdot x_0}{1-\bar{\alpha}_t}$$

Replacing $x_0$ above using Eq. 1.

$$\mu_q(x_t, x_0) = \frac{\sqrt{\alpha_t},(1-\bar{\alpha}_{t-1})\cdot x_t + \sqrt{\bar{\alpha}_{t-1}},(1-\alpha_t)\cdot \overbrace{\left(\dfrac{x_t - \sqrt{1-\bar{\alpha}_t},\epsilon_t}{\sqrt{\bar{\alpha}_t}}\right)}^{x_0}}{1-\bar{\alpha}_t}$$

$$\mu_q(x_t, \epsilon_t) = \frac{1}{\sqrt{\alpha_t}}\cdot x_t - \frac{1-\alpha_t}{\sqrt{1-\bar{\alpha}_t}\cdot\sqrt{\alpha_t}}\cdot \epsilon_t$$

$$\mu_\theta(x_t) = \frac{1}{\sqrt{\alpha_t}}\cdot x_t - \frac{1-\alpha_t}{\sqrt{1-\bar{\alpha}_t}\cdot\sqrt{\alpha_t}}\cdot \hat{\epsilon}_\theta(x_t)$$

Consistency term $= \dfrac{1}{2\sigma_q^2}|\mu_q - \mu_\theta|_2^2$

$$= \frac{1}{2\sigma_q^2} \cdot \frac{(1-\alpha_t)^2}{(1-\bar{\alpha}_t),\alpha_t} \left[|\epsilon_t - \hat{\epsilon}_\theta(x_t)|_2^2\right]$$

$$\propto |\epsilon_t - \hat{\epsilon}_\theta(x_t)|_2^2$$

This problem can be seen as now **Regression over the added noise**
Earlier we were taking x_t and predicting the mean of distribution x_t-1 given x_t and x_o . now we will directly predict the noise that was added to x_o to make it x_t. This is interpretations as seen in the original paper [[DDPM Original Paper]]
## Diagram

$$x_{t,, t} \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \ \text{dim}};\theta;\substack{\text{increase} \ \text{dim}}} \rightarrow \hat{\epsilon}_\theta(x_t) \qquad |\epsilon_t - \hat{\epsilon}_\theta(x_t)|_2^2$$

$\hookrightarrow$ Regressor on the added noise