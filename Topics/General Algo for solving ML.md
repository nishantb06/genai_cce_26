**Goal:** Given $\mathcal{D}$, estimate and sample from $P_X$.

### Steps

1. **Parametric model:** Choose a functional form $P_\theta$ (typically a Neural Network).

$$P_\theta(x) = \sigma(W_3(\sigma(W_2(W_1 x)))) \quad \text{(composition of linearities + nonlinearities)}$$

where $\theta = \{W_1, W_2, W_3, \ldots\}$.

> Universal function approximation via sigmoid activations.

2. **Define a distance** between $P_X$ and $P_\theta$: call it $D(P_X, P_\theta)$ called [[F-Divergence]]

3. **Optimise $\theta$** to minimise the distance:

$$\hat{\theta} = \arg\min_\theta D(P_X, P_\theta) \quad \text{(Training)}$$

Such that $P_{\hat{\theta}} \approx P_X$.

### Important Questions

- (a) How to compute $D(P_X, P_\theta)$ without knowing $P_X$?
- (b) How to solve the optimisation?
- (c) What parametric form to choose for $P_\theta$?
- (d) How to sample from $P_\theta$?