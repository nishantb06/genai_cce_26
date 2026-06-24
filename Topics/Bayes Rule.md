$$p(x \mid y) = \frac{p(y \mid x)\, p(x)}{p(y)} = \frac{p(y \mid x)\, p(x)}{\int p(y \mid x)\, p(x)\, \mathrm{d}x}$$

$$= \frac{p(x, y)}{p(y)} = \frac{p(x, y)}{\sum_i p(x_i, y)}$$
---
$$\underbrace{p(x \mid y)}_{\text{posterior}} = \frac{\overbrace{p(y \mid x)}^{\text{likelihood}}\; \overbrace{p(x)}^{\text{prior}}}{\underbrace{p(y)}_{\text{evidence}}}$$

$$\underbrace{p(x \mid y)}_{\text{conditional probability}} = \frac{\overbrace{p(x, y)}^{\text{joint generative model}}}{\underbrace{p(y)}_{\text{marginal probability}}} = \frac{\overbrace{p(y \mid x)\, p(x)}^{\text{product rule}}}{\underbrace{\sum_i p(y \mid x_i)\, p(x_i)}_{\text{sum rule}}}$$
