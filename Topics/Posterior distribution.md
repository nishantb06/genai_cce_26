$$\underbrace{p(x \mid y)}_{\text{posterior}} = \frac{\overbrace{p(y \mid x)}^{\text{likelihood}}\; \overbrace{p(x)}^{\text{prior}}}{\underbrace{p(y)}_{\text{evidence}}}$$

$$\underbrace{p(x \mid y)}_{\text{conditional probability}} = \frac{\overbrace{p(x, y)}^{\text{joint generative model}}}{\underbrace{p(y)}_{\text{marginal probability}}} = \frac{\overbrace{p(y \mid x)\, p(x)}^{\text{product rule}}}{\underbrace{\sum_i p(y \mid x_i)\, p(x_i)}_{\text{sum rule}}}$$

![[images/Pasted image 20260618194405.png]]
Summing along the axes gives us the [[Marginal Distribution]] , then how do we get the posterior ?

We take the p(y) and do a broadcast divide along all the rows 

Related
[[Prior distribution]]
[[Conditional Probability Distribution]]
[[Likelihood]]
