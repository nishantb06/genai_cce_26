# Vector Quantized VAE (VQ-VAE)

In VQ-VAE, the latent space is discrete & vector-quantized using a learnable dictionary.

Unlike in a VAE , in in VQ-VAE we get the samples from the latent posterior not the parameters itself (read [[How to represent probability distributions via Neural Networks]] )

It has a deterministic encoder. 
## Diagram

$$\left\{ z_1, z_2, \ldots, z_M \right\} \text{ : lat. Dictionary}$$
M/p Latent vectors of k dimension each
$$x_i \rightarrow \underbrace{q_\phi}_{\text{Enc.}} \rightarrow \hat{z}_e(x_i) \quad \hat{z}_q(x_i) \rightarrow \underbrace{p_\theta}_{\text{Dec.}} \rightarrow \hat{x}_i$$

$$z_i \in \mathbb{R}^k, \quad \hat{z}_e(x_i) \in \mathbb{R}^{k \times p} \text{ : } p\text{-vectors from the lat. dict.}$$

Suppose there are $M$ latent vectors of $k$-dim each in the dictionary.

$$L = \left\{ z_1, z_2, \ldots, z_M \right\}, \quad z_i \in \mathbb{R}^k$$

$$z_q(x_i) = z_{j^*}, \quad j^* = \underset{j=1,\ldots,M}{\mathrm{argmin}} \|z_e(x_i) - z_j\|_2^2$$

$z_e(x_i)$ : column of $\hat{z}_e(x_i)$ $\qquad \hookrightarrow$ vector quantization

Choose that vector from the latent dictionary which is closest to the sample generated from the latent posterior. This vector now goes into the decoder as input. 
In practice, the latent space is designed to be a tensor of latent dictionary.

---

$$\hat{z}_e(x_i) = \begin{bmatrix} | & | & | & | & | & | \\ & & & & & \\ | & | & | & | & | & | \end{bmatrix}_{k \times p}$$

Each row is a vector from the $k \times p$ dictionary $L$.

Each column of $\hat{z}_e(x_i)$ is vector quantized.

---

## Training a VQ-VAE

$$J_\theta(q) = \|x - \hat{x}_\theta(\hat{z}_q)\|_2^2 + \|z_e(x_i) - z_q(x)\|_2^2$$

In addition to the Encoder & Decoder parameters, the latent dictionary is also learned.

$$z_j^{t+1} \leftarrow z_j^t - \alpha \, \nabla_{z_j}\left(J_\theta(q)\right)$$

---

## Inference in a VQ-VAE

### a) Embedding Extraction / Posterior Inference

$$x_\text{test} \rightarrow q_{\phi^*} \rightarrow \hat{z}_e(x_\text{test}) \in \mathbb{R}^{k \times p}$$

$$\hat{z}_q(\text{test}) = \underset{j=1,\ldots,M}{\mathrm{argmin}} \|\hat{z}_e(x_\text{test}) - z_j\|_2^2$$

## b) Sampling in VQ-VAE

$$\hat{z}_q(x) \rightarrow p_{\theta^*} \rightarrow \hat{x}_\theta$$

To be able to sample from the decoder of VQ-VAE, we need to sample from the distribution of $\hat{z}_q(\cdot)$.

To learn to sample from the dist. of $\hat{z}_q(\cdot)$, a generative model is fit to samples of $z_q$. E.g. GMM on the samples from the o/p of Encoder corresponding to all training datapoints.

Sample from the learned distribution of $z_q$ & use it as the input to the Decoder.


**VQ-VAE's are best used for learning the latent space / embedding extraction not for generation!**


