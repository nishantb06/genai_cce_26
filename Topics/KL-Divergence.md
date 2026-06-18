$$D_{\mathrm{KL}}(P_X \| P_\theta) = \int_{\mathcal{X}} p_X(x) \log \frac{p_X(x)}{p_\theta(x)}\, dx$$

Expanding:

$$= \int p_X \log p_X\, dx - \int p_X \log p_\theta\, dx$$

The first term is the [[Self Entropy]] and the 2nd part is the [[Cross Entropy]].
The first term is constant w.r.t. $\theta$, so:

$$\hat{\theta} = \arg\min_\theta D_{\mathrm{KL}}(P_X \| P_\theta) = \arg\max_\theta \int p_X \log p_\theta\, dx$$

This is the **[[Maximum Likelihood Estimation]] (MLE)**.

### Computing the Expectation via Samples
One important thing to keep in mind while mathematical manipulation is to get to the form where we can represent our [[Integrals in terms of expectations]]

$$\int p_X(x) \log p_\theta(x)\, dx = \mathbb{E}_{x \sim p_X}[\log p_\theta(x)]$$

**[[Weak Law of Large Numbers ]]** Given $\mathcal{D} = \{x_i\} \overset{\text{iid}}{\sim} p_X$, for any function $g$:

$$\frac{1}{N}\sum_{i=1}^{N} g(x_i) \xrightarrow[N \to \infty]{} \mathbb{E}[g(x)]$$

Therefore:

$$\boxed{\hat{\theta} = \arg\min_\theta D_{\mathrm{KL}}(P_X \| P_\theta) = \arg\max_\theta \frac{1}{N} \sum_{i=1}^{N} \log p_\theta(x_i)}$$
Related
1. [[Sampling from a distribution]]