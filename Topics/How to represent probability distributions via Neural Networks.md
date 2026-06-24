w## a) Deterministic representation.

GAN generator

$$z \sim \mathcal{N}(0, I) \longrightarrow \boxed{g_\theta(z)} \longrightarrow \hat{x} \sim p_\theta(\hat{x})$$

outputs the samples from the dist. that it models.

$$x \longrightarrow \boxed{\text{classifier}} \longrightarrow y \mid x \sim p(y \mid x)$$

---

## b) probabilistic representation.

$$x \longrightarrow \boxed{q_\phi(z \mid x)} \longrightarrow \text{parameters of } q(z \mid x)$$

outputs the parameters of the distribution that it models, but not the samples from it.

---

In a [[VAEs]], the distributions $q(z \mid x)$ & $p(x \mid z)$ are represented using probabilistic NNs.
