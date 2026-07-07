
The basic idea : Build DMs on the latent space induced by another Encoder-Decoder Models.

Given data $x_0 \in \mathbb{R}^d \sim p(x_0)$, the first step is to learn a latent representation $z_0 \in \mathbb{R}^k$, $k \ll d$, using an Enc-Dec Model.

**E.g.:** Construct a VQ-VAE to learn a latent space.

## Diagram

$$x_0 \xrightarrow{E_\phi} z_0 \xrightarrow{D_\theta} \hat{x}_0$$

Let $E_\phi$, $D_\theta$ represent the Encoder & Decoder functions, respectively.

$E_{\phi^*}$ & $D_{\theta^*}$ are trained using the original data $x_0$ or some other dataset similar to $x_0$.

All the datapoints in $\mathbb{R}^d$, are projected on to the latent space as $z_0 = E_{\phi^*}(x_0)$.

A DDPM is constructed on the space of $z_0$.

During inference, to generate a novel point from $p(x_0)$, first sample a novel point from the latent space with reverse diffusion, then decode:

$$
\begin{aligned}
z_{\text{novel}} &\leftarrow \text{reverse diffusion}, \\
x_{\text{novel}} &= D_{\theta^*}(z_{\text{novel}}) \sim p(x_0).
\end{aligned}
$$
Advantage over [[Denoising Diffusion Probabilistic Models (DDPM) | DDPM]] is that we are learning a DDPM on a much more compact latent space as compared to the high dimensional data space . 

But this required a strong Encoder Decoder model pre trained. 
This is much more empirically stable and hence called [[Stable Diffusion]]