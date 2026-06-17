Let $\theta_t$ and $q_t$ represent the estimates at iteration $t$.

**For** $t = 1$ **to** $T$:

**E-step** (fix $\theta^t$, optimise over $q$):

$$q_{t+1}^* = \arg\max_q ; J_{\theta^t}(q), \quad \text{with } \theta^t \text{ held constant}$$

**M-step** (fix $q_{t+1}$, optimise over $\theta$):

$$\theta_{t+1}^* = \arg\max_\theta ; J_\theta(q_{t+1}), \quad \text{with } q_{t+1} \text{ held constant}$$

> It can be shown that EM ensures the log-likelihood is non-decreasing: $$\ell(\theta_{t+1}) \geq \ell(\theta_t)$$

