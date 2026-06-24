$x_i \in \mathbb{R}^d$, $z_i \in \mathbb{R}^k$, $\mu_\phi(x) \in \mathbb{R}^k$, $\Sigma_\phi(x_i) \in \mathbb{R}^{k \times k}$

Sigma is a diagonal matrix where every element except the diagonal is 0.
For the same x_i there can be multiple latent vectors using the reparameterization trick.

$x_i \longrightarrow \boxed{q_\phi(z \mid x)} \longrightarrow \begin{cases} \mu_\phi(x_i),\, \Sigma_\phi(x_i) \end{cases} \longrightarrow \boxed{p_\theta(x \mid z)} \longrightarrow \hat{x}_\theta(z_i)$ params of $p_\theta(x \mid z)$

$\varepsilon_i \sim \mathcal{N}(0, I)$, $z_i = \mu_\phi(x_i) + \Sigma_\phi(x_i) \cdot \varepsilon_i$ $\leftarrow$ accomplished using reparameterization.

wanted $\longrightarrow$ $z_i \sim q_\phi(z \mid x) = \mathcal{N}\left(\mu_\phi(x_i),\, \Sigma_\phi(x_i)\right)$

$$\nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) = \nabla_\phi \mathbb{E}_{P_\varepsilon} \log p_\theta\left(x \mid g(\varepsilon)\right)$$

$$= \nabla_\phi \left( \frac{1}{M} \sum_{j=1}^{M} \log p_\theta\left(x \mid g(\varepsilon_j)\right) \right), \quad \varepsilon_1, \varepsilon_2, \ldots, \varepsilon_M \sim P_\varepsilon$$

---

## To compute $\log p_\theta\left(x \mid g(\varepsilon_j)\right)$ :

Multiple ways to do this, 
parameterise $p_\theta(x \mid z)$ via some known distribution & use the Decoder to output its parameters.

Eg: $p_\theta(x \mid z) = \mathcal{N}\left(\hat{x}_\theta(z),\, I\right)$

With the above,

$$\log p_\theta(x \mid z) = \log \left( \frac{1}{(2\pi)^{d/2}} \exp\left( -\frac{1}{2} \| x - \hat{x}_\theta(z) \|_2^2 \right) \right)$$

$$\propto -\frac{1}{2} \| x - \hat{x}_\theta(z) \|_2^2$$
This is where the [[Reconstruction Loss]] comes into picture. The output of the decoder and the input image should match on a pixel level
$\implies$

$$\nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) =$$

$$\nabla_\phi \mathbb{E}_{P_\varepsilon} \log p_\theta\left(x \mid g(\varepsilon)\right) =$$

$$\nabla_\phi \left[ \frac{1}{M} \sum_{j=1}^{M} \| x_i - \hat{x}_\theta(z_j) \|_2^2 \right]$$

where $z_j = \mu_\phi(x_i) + \Sigma_\phi(x_i) \cdot \varepsilon_j$

$$\varepsilon_1, \ldots, \varepsilon_M \sim \mathcal{N}(0, I)$$

---

![[images/Pasted image 20260622215112.png]]

> $\theta$ is fixed  
> $p_\theta(x \mid z) \rightarrow \hat{x}_\theta(z_i)$  
> $\frac{1}{M} \sum \|x_i - \hat{x}_\theta(z_j)\|_2^2$  
> $\nabla_\phi \left( \frac{1}{M} \sum \|x_i - \hat{x}_\theta(z_j)\|_2^2 \right)$

---

## Forward Pass

**i)** Given an $x_i \in \mathcal{D}$, pass it through the Encoder to obtain $\mu_\phi(x_i)$ & $\Sigma_\phi(x_i)$

**ii)** Sample $\varepsilon_1, \ldots, \varepsilon_M \sim \mathcal{N}(0, I)$ outside the NNs.

**iii)** Compute $z_1 \ldots z_M$ via reparameterization.

**iv)** Pass all of $z_1 \ldots z_j$ through the Decoder to compute $\hat{x}_\theta(z_j)$ 

**v)** Compute

$$-\frac{1}{M} \sum_{j=1}^{M} \|x_i - \hat{x}_\theta(z_j)\|_2^2$$

---

## Backward Pass

**i)** Compute the grad $\nabla_\phi \left( \frac{-1}{M} \sum_{j=1}^{M} \|x_i - \hat{x}_\theta(z_j)\|_2^2 \right)$

**ii)** Back prop through these 3 things
- Decoder, with fixed parameters $\theta$
- Reparam, Id of $\phi$
- Encoder,

---

> Thus, we obtain the $\nabla_\phi \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z)$

---

To compute $\nabla_\phi D_{\mathrm{KL}}\left[ q_\phi(z \mid x) \,\|\, p_\theta(z) \right]$

---

$p_\theta(z)$ : Latent prior, typically assumed to be $\mathcal{N}(0, I)$

$$q_\phi(z \mid x) = \mathcal{N}\left(\mu_\phi(x),\, \Sigma_\phi(x)\right)$$

$$\therefore D_{\mathrm{KL}}\left[ q_\phi(z \mid x) \,\|\, p_\theta(z) \right]$$

$$= D_{\mathrm{KL}}\left[ \mathcal{N}\left(\mu_\phi(x),\, \Sigma_\phi(x)\right) \,\|\, \mathcal{N}(0, I) \right]$$

$$= \frac{1}{2} \left[ \mathrm{tr}\left(\Sigma_\phi(x)\right) + \|\mu_\phi(x)\|_2^2 - k - \log \left|\Sigma_\phi(x)\right| \right] \quad \text{: Can be estimated analytically}$$
trace ,determinant all are scalar
the entire term is a scalar

Can be estimated because the KL Divergence between two gaussians can be calculated analytically. 


$$\therefore \nabla_\phi D_{\mathrm{KL}}\left[ q_\phi(z \mid x) \,\|\, p_\theta(z) \right]$$

$$\nabla_\phi \left[ \frac{1}{2} \left( \mathrm{tr}\left(\Sigma_\phi(x)\right) + \|\mu_\phi(x)\|_2^2 - k - \log \left|\Sigma_\phi(x)\right| \right) \right] = \nabla_\phi (\mathrm{KL})$$

this gradient wrt the KL is simply added to the gradients of the first term that we calculated earlier. 

---

$$\phi^{t+1} \leftarrow \phi^t + \alpha \, \nabla_\phi J_\theta(q_\phi)$$

This is one training step for the Encoder

To train the decoder, we can just ignore the KL term, because it is independent of theta

# Training the Decoder

$$\nabla_\theta J_\theta(q_\phi) = \nabla_\theta \left[ \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) \right]$$

$$\nabla_\theta \left[ D_{\mathrm{KL}}\left[ q_\phi(z \mid x) \,\|\, p_\theta(z) \right] \right] = 0$$

---

To find $\nabla_\theta \left[ \mathbb{E}_{q_\phi(z \mid x)} \log p_\theta(x \mid z) \right]$

---

## Diagram

> $\phi$ is a constant

$$q_\phi(z \mid x) \rightarrow \mu_\phi(x_i)$$

$$x_i \rightarrow \quad \rightarrow \Sigma_\phi(x_i)$$

$$\varepsilon_1, \ldots, \varepsilon_M \sim \mathcal{N}(0, I)$$

$$z_j = \mu_\phi(x_i) + \Sigma_\phi(x_i) \cdot \varepsilon_j \qquad j = 1, \ldots, M$$

> $p_\theta(x \mid z) \rightarrow \hat{x}_\theta(z_i)$  
> $\frac{1}{M} \sum \|x_i - \hat{x}_\theta(z_j)\|_2^2$  
> $\nabla_\theta \left( \frac{1}{M} \sum \|x_i - \hat{x}_\theta(z_j)\|_2^2 \right)$

---

$$\theta^{t+1} \leftarrow \theta^t + \alpha \, \nabla_\theta J_\theta(q_\phi)$$

This is one training step for the Decoder



----
## Recap on Training of a VAE

Given $\mathcal{D} = \left{ x_i \right}_{i=1}^n \sim \text{iid } P_x$, $\quad x \in \mathbb{R}^d,, z \in \mathbb{R}^k$, $\quad k \ll d$


$$x \xrightarrow{\text{d-dim}} \underbrace{q_\phi(z|x)}_{\text{Enc}} \xrightarrow{k} \mu_\phi(x)$$

$$\xrightarrow{k} \begin{bmatrix} \sigma_1 \ \sigma_1 \ \vdots \ \sigma_k \end{bmatrix} \xrightarrow{z_j,; k\text{-dim}} p_\theta(x|z) \xrightarrow{\hat{x}_\theta(z),; d\text{-dim}}$$

$$\underbrace{\hspace{2cm}}_{\text{Enc}} \hspace{3cm} \underbrace{\hspace{2cm}}_{\text{Dec}}$$

$$\Sigma_\phi(x) = \mathrm{diag}\left([\sigma_1 \ldots \sigma_k]\right)$$

$$\epsilon_1 \ldots \epsilon_M \sim \mathcal{N}(0, I)$$

$$z_j = \mu_\phi(x) + [\sigma_1 \ldots \sigma_k]^T \cdot I \odot \epsilon_j \qquad \text{Reparam.}$$

---

Typically, $q_\phi(z|x) \sim \mathcal{N}!\left(z;, \mu_\phi(x),, \Sigma_\phi(x)\right)$

$$\Sigma_\phi(x) = \mathrm{diag}\left(\sigma_1, \sigma_2 \ldots \sigma_k\right)$$

---

This is the [[Evidence Lower Bound | ELBO]] for [[VAEs]]
$$J_\theta(q_\phi) = \mathbb{E}_{q_\phi(z|x)} \log p_\theta(x|z) - D_{KL}\left[q_\phi(z|x) ,|, p(z)\right]$$

$$= \left|x - \hat{x}_\phi(z)\right|_2^2 - \left(\frac{-1}{2} \log \left|\Sigma_\phi(x)\right| - k + \mathrm{tr}\left(\Sigma_\phi(x)\right) + |\mu_\phi(x)|_2^2\right)$$

---

$\theta$ & $\phi$ are updated alternatively via gradient descent.

Next read [[Inference with a trained VAE]]