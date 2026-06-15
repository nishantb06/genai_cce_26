## Definition

Given two probability distribution functions with corresponding density functions denoted by $p_X$ and $p_\theta$, the **f-divergence** between them is defined as:

$$D_f\left(P_X | P_\theta\right) = \int_{\mathcal{X}} p_\theta(x), f\left(\frac{p_X(x)}{p_\theta(x)}\right) dx$$

**Where:**

- $f(u) : \mathbb{R}^+ \to \mathbb{R}$ — convex, left-semi-continuous function with $f(1) = 0$
- $\mathcal{X}$ — space on which $P_X$ and $P_\theta$ are supported

---

## Properties of f-Divergence

**i)** $D_f(\cdot) \geq 0$ for any choice of $f(\cdot)$. This is called [[Jensen's inequality]]

**ii)** $D_f(P_X | P_\theta) = 0 \iff P_X = P_\theta$.

> **[[Convexity condition]]:** A function $f(u)$ is convex iff $\forall, u_1, u_2 \in U$ and $0 \leq \alpha_1, \alpha_2 \leq 1$: $$\alpha_1 f(u_1) + \alpha_2 f(u_2) \geq f(\alpha_1 u_1 + \alpha_2 u_2)$$
---

## Examples of f-Divergence

By changing the inherent function f we can get various distance metrics between two distributions. Is there any limitations on what that function can be ? like does it have to be convex ? does it have to be bounded? etc

[[Constraints on the choice of the f function]]
### i) [[KL-Divergence]]   : $f(u) = u \log u$

$$D_f!\left(P_X | P_\theta\right) = \int_{\mathcal{X}} p_\theta(x), f!\left(\frac{p_X(x)}{p_\theta(x)}\right) dx$$

$$= \int_{\mathcal{X}} p_\theta(x) \left[\frac{p_X(x)}{p_\theta(x)} \cdot \log \frac{p_X(x)}{p_\theta(x)}\right] dx$$

$$= \int_{\mathcal{X}} p_X(x) \log \frac{p_X(x)}{p_\theta(x)}, dx = D_{\mathrm{KL}}$$

> **Note:** KL-divergence is **asymmetric**: $$D_{\mathrm{KL}}(P_X | P_\theta) \neq D_{\mathrm{KL}}(P_\theta | P_X)$$
> 
> - $D_{\mathrm{KL}}(P_X | P_\theta)$ — **Forward KL**
> - $D_{\mathrm{KL}}(P_\theta | P_X)$ — **Reverse KL**

---

### ii) [[Jenson Shannon Divergence | JS-Divergence]] — $f(u) = \dfrac{1}{2}\left(u \log u - (u+1)\log\dfrac{u+1}{2}\right)$

$$D_{\mathrm{JS}}(P_X | P_\theta) = D_f(P_X | P_\theta) \quad \text{with the above } f$$

---

### iii) [[Total Variation Distance ]]— $f(u) = \dfrac{1}{2}|u - 1|$

$$D_{\mathrm{TV}}(P_X | P_\theta) = D_f(P_X | P_\theta) \quad \text{with } f(u) = \tfrac{1}{2}|u-1|$$

---

## Tags

#f-divergence #KL-divergence #JS-divergence #total-variation #generative-modelling #probability #machine-learning
