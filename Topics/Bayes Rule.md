Allows us to switch the order of conditioning

According to this definition, the conditional probability of AA given BB is the ratio of P[A∩B]P[A∩B] to P[B]P[B]. It is the probability that AA happens when we know that BB has already happened. Since BB has already happened, the event that AA has also happened is represented by A∩BA∩B. However, since we are only interested in the relative probability of AA with respect to BB, we need to normalize using BB. This can be seen by comparing P[A∣B]P[A∣B] and P[A∩B]P[A∩B]:

$$p(x \mid y) = \frac{p(y \mid x)\, p(x)}{p(y)} = \frac{p(y \mid x)\, p(x)}{\int p(y \mid x)\, p(x)\, \mathrm{d}x}$$

$$= \frac{p(x, y)}{p(y)} = \frac{p(x, y)}{\sum_i p(x_i, y)}$$
---
$$\underbrace{p(x \mid y)}_{\text{posterior}} = \frac{\overbrace{p(y \mid x)}^{\text{likelihood}}\; \overbrace{p(x)}^{\text{prior}}}{\underbrace{p(y)}_{\text{evidence}}}$$

$$\underbrace{p(x \mid y)}_{\text{conditional probability}} = \frac{\overbrace{p(x, y)}^{\text{joint generative model}}}{\underbrace{p(y)}_{\text{marginal probability}}} = \frac{\overbrace{p(y \mid x)\, p(x)}^{\text{product rule}}}{\underbrace{\sum_i p(y \mid x_i)\, p(x_i)}_{\text{sum rule}}}$$

P(b | a) is called conditional probabilty , P(A | B) is called Posterior probablity. A and B can be swapped depends on context. 