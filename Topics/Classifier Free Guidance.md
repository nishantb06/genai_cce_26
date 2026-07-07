
$$\nabla \log p(x_t \mid y) = \nabla \log p(x_t) + \nabla \log p(y \mid x_t)$$

$$\nabla \log p(y \mid x_t) = \nabla \log p(x_t \mid y) - \nabla \log p(x_t)$$
$$\nabla \log p(x_t \mid y) \approx \nabla \log p(x_t) + \lambda\left(\nabla \log p(x_t \mid y) - \nabla \log p(x_t)\right)$$

$$\boxed{\nabla_{x_t} \log p(x_t \mid y) = \lambda, \nabla_{x_t} \log p(x_t \mid y) + (1-\lambda), \nabla_{x_t} \log p(x_t)}$$

$\lambda$ : hyper-parameter

---

## Diagram

$$y,\; x_{t},t \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \ \text{dim}};\theta;\substack{\text{increase} \ \text{dim}}} \rightarrow$$

$\hookrightarrow$ Regressor over $\nabla_{x_t} \log p(x_t \mid y)$

null label / text $\downarrow$

$$y = \phi,; x_{t,t} \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \ \text{dim}};\theta;\substack{\text{increase} \ \text{dim}}} \rightarrow \quad \text{(copy of the above)}$$

$\hookrightarrow$ Regressor over $\nabla_{x_t} \log p(x_t)$

& add both the $(\lambda)$ cond. & $(1-\lambda)$ uncond. scores before the gradient step.

pass it through the NN once with the y and once without the y that is the null text / null label

This is actually the SOTA for conditional image generation. 