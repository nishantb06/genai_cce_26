

--- 
Change in Notation
$X_o$ data variable , $P_{X_O}$ is the original data distribution
$X_1, X_2 ... X_T$  are the latent variables

---


Given Data $\mathcal{D} = {x_0} \sim P_{x_0}$ (data distribution)

**Goal:** To learn to sample from $P_{x_0}$ (Gen. AI)

DDPMs are latent variable Generative Models seen as special case of hierarchical VAEs.

Recall, in a VAE,

$$X \xrightarrow[\text{Data}]{\quad} \xrightarrow{q(z|x)}_{\text{Enc.}} Z_{\downarrow \text{latent}} \xrightarrow{p(x|z)}_{\text{Dec.}} X_{\downarrow \text{Data}}$$

In a HVAE (Hierarchical VAE), there are multiple latent spaces.
$T$ number of latent spaces

$$X \rightarrow Z_1 \rightarrow Z_2 \rightarrow Z_3 \rightarrow \ldots \rightarrow Z_T \quad \text{(Encoding)}$$

$$Z_T \rightarrow Z_{T-1} \rightarrow Z_{T-2} \rightarrow \ldots \rightarrow X \quad \text{(Decoding)}$$

A DDPM is a h-VAE, with the following properties: (Hierarchical VAE)

**a)** **There are multiple latent spaces**. In VAE's we force the single latent space to encode all the information about the data space. It makes more sense to have multiple latent space encode information about the original data

$$z_1, z_2 \ldots, z_T$$
**b)** **The dimensionality of all the latent spaces is same as that of the data space.** 

$$\dim(z_t) = \dim(x) \quad \forall\, t$$

**c)** **The Encoding procedure is fixed or non-learnable unlike a VAE**.
Encoding procedure is not deterministic, it is probabilistic but non-learnable in a DDPM.

- VAE : $q_\phi(z|x)$ : $\phi$ is a NN that learned
    
- DDPM : $q(z|x)$ : is fixed & not learnable.
    
- VAE : both Encoding & Decoding are learned
    
- DDPM : only decoding is learned.
    
A lot of the maths comes from the [[Stochastic Differential Equations]] field of Mathematics. Here the belief is that if we can learn to go from a data space to latent space then perhaps we can learn to go from latent space to data space. In doing so we would have a generative model

---

## DDPM Formulation

**Notations:**

- Data variable is denoted by $x_0$ $(x)$
- Latent space : $x_1, x_2 \ldots, x_T$ $(z_1, z_2 \ldots, z_T)$

(not be to confused with previous notations where $x_1, x_2 \ldots$ were data points)

In the DDPM literature, $x_0$ : data point

$x_1, x_2 \ldots, x_T$ : latent spaces / vectors


# Encoding / Forward Process

$$x_0 \rightarrow x_1 \rightarrow x_2 \rightarrow \ldots \rightarrow x_T$$

- $x_0$ : data point
- $x_1 \ldots x_T$ : latent vectors corresponding to $x_0$

$$\dim(x_t) = \dim(x_0) \equiv \mathbb{R}^d \quad \forall \, t$$

$T$ : hyperparameter

---
 
## Define the Encoding / Forward /Noising Process in DDPM

The next latent variable is the scaled and shifted version of the previous latent variable. Scale is determined by $\alpha$ and shift by $\epsilon$ which is drawn from a Unit gaussian distribution.  

$$x_1 = \sqrt{\alpha_1}\, x_0 + \sqrt{1-\alpha_1}\, \epsilon_1 \qquad \epsilon_1 \sim \mathcal{N}(0, I)$$

$$x_2 = \sqrt{\alpha_2}\, x_1 + \sqrt{1-\alpha_2}\, \epsilon_2 \qquad \epsilon_2 \sim \mathcal{N}(0, I)$$

$$x_t = \sqrt{\alpha_t}\, x_{t-1} + \sqrt{1-\alpha_t}\, \epsilon_t \qquad \epsilon_t \sim \mathcal{N}(0, I)$$

where $\alpha_1 \ldots \alpha_T$ are fixed scalars $\in [0, 1]$

Scale the noise and the datapoint to adhere to a schedule 

---

## Diagram
![[Pasted image 20260627122118.png]]


---

$x_0$ Data $\rightarrow$ add noise $\rightarrow$ $x_1$ noisy data $\rightarrow$ add noise $\rightarrow$ $x_2$ noisy-noisy data $\rightarrow \ldots \rightarrow$ "noise only" $x_T$

$$x_t = \sqrt{\alpha_t}, x_{t-1} + \sqrt{1-\alpha_t}, \epsilon_t \qquad \epsilon_t \sim \mathcal{N}(0, I) \quad -(1)$$

The above defines the Encoding or the Forward process of a DDPM.

Eq. (1) : represents a 1st order [[Markov Chain]] with Gaussian transitions

1st order Markov Chain defines a series of RVs, $x_0, x_1 \ldots x_T$ s.t

$$x_t \perp\!\!\!\perp x_{t-2} \ldots x_0 \mid x_{t-1}$$

$\Rightarrow$ This implies One can define a series of conditional distributions on the latent variables as:

$$q\left(x_t \mid x_{t-1}\right) = \mathcal{N}\!\left(x_t;\; \underbrace{\sqrt{\alpha_t}\, x_{t-1}}_{\text{mean}}\,; \underbrace{(1-\alpha_t)\, I}_{\text{var}}\right)$$

because,

$$x_t = \sqrt{\alpha_t}\, x_{t-1} + \sqrt{1-\alpha_t}, \epsilon_t \qquad \epsilon_t \sim \mathcal{N}(0, I)$$

$q\left(x_t \mid x_{t-1}\right)$ : conditional forward / Encoding distributions. Note that x_t-1 is fixed here

$q(x_T) \sim \mathcal{N}(0, I)$ : [[Stationary distribution of the Markov Chain]]
**The last conditional forward distribution will converge to a Gaussian with 0 mean and Unit variance !** For this T ~ 1000 steps
# Define the Model via a Decoding Distribution

From the [[Chain rule of probability]] and the properties of the first order MC
namely "once you know the current state ​, earlier future states contain no additional information."
$$p_\theta\left(x_0, x_1, x_2 \ldots, x_T\right) = p_\theta(x_T) \prod_{t=1}^{T} p_\theta\left(x_{t-1} \mid x_t\right)$$

$$\underbrace{x_0}_{\text{data}} \quad \underbrace{x_1 \ldots x_T}_{\text{lat. var}}$$

where $p_\theta\left(x_{t-1} \mid x_t\right) \triangleq \mathcal{N}\!\left(x_{t-1};; \mu_\theta(x_t),, \Sigma_\theta(x_t)\right)$

$p_\theta$ defines a latent variable model over the [[Joint Distribution]] with multiple latent variables, similar to VAE, where we define $p_\theta(x, z)$ : joint distributions  b/w data & lat. var.

The definition of the model distribution $p_\theta(\cdot)$ in a DDPM, arises because of the Markovian (1st order) assumption in the reverse direction, with Gaussian transitions containing learnable parameters.

Decoding process is also a Markov chain in the reverse direction. The catch here is that the mean and variance of every transitional distribution is learnable

$$p_\theta\left(x_{t-1} \mid x_t\right) \triangleq \mathcal{N}\!\left(x_{t-1};\; \mu_\theta(x_t),\, \Sigma_\theta(x_t)\right)$$

$\mu_\theta(x_t)$ & $\Sigma_\theta(x_t)$ are learned via ELBO.

# [[Evidence Lower Bound | ELBO]] Optimization to Learn the Decoding Parameters in a DDPMc

Recall, in a VAE,

$$\log p_\theta(x) = \log \int_z p_\theta(x, z)\, dz$$

$$J_\theta(q_\phi) = \mathbb{E}_{q_\phi(z|x)} \log \frac{p_\theta(x, z)}{q_\phi(z|x)} \quad \text{: Evidence Lower Bound (ELBO)}$$

In a DDPM,

$$J_\theta(q)^{\text{DDPM}} = \mathbb{E}_{q(x_1, x_2 \ldots x_T | x_0)} \log \frac{p_\theta(x_0, x_1, x_2 \ldots, x_T)}{q(x_1, x_2 \ldots x_T | x_0)}$$

$$\boxed{J_\theta(q)^{\text{DDPM}} = \mathbb{E}_{q(x_{1:T} \mid x_0)} \log \frac{p_\theta(x_{0:T})}{q(x_{1:T} \mid x_0)}}$$

$$x_{1:T} = \left(x_1, x_2, \ldots, x_T\right) \qquad x_{0:T} = \left(x_0, x_1, \ldots, x_T\right)$$

# Optimising the ELBO for DDPM

$$J_\theta(q)^{\text{DDPM}} = \mathbb{E}_{q(x_{1:T} \mid x_0)} \log \frac{p_\theta(x_{0:T})}{q(x_{1:T} \mid x_0)}$$

We have,

$$p_\theta(x_{0:T}) = p(x_T) \prod_{t=1}^{T} p_\theta\left(x_{t-1} \mid x_t\right)$$
The above equation comes again from the [[Chain rule of probability]]
$$p(x_T) = \mathcal{N}(0, I)$$
Because the Stationary distribution of a 1st order MC is a Gaussian Distribution. 
Similarly,

$$q(x_{1:T} \mid x_0) = \prod_{t=1}^{T} q\left(x_t \mid x_{t-1}\right)$$
Because the forward or the encoding process is a first order Markovian and from the [[Chain rule of probability]]

---

$$q(x_{1:T} \mid x_0) = q(x_1 \mid x_0)\,  q(x_2 \mid x_1, x_0)\, q(x_3 \mid x_2, x_1, x_0)$$

$$\cdots, q\left(x_T \mid x_{T-1}, x_{T-2} \ldots x_0\right)$$
This is from the original formulation of the Chain rule of probability but when we consider the property of MC that one event is only depenedent on the previous one
$$= \prod_{t=1}^{T} q\left(x_t \mid x_{t-1}\right)$$

$\because$ the forward / Encoding is first order Markov
$$\therefore\quad J_\theta(q) = \mathbb{E}_q \log \frac{p_\theta(x_{0:T})}{q(x_{1:T} \mid x_0)}$$
The denominator is the posterior of latents conditioned on the data
$$= \mathbb{E}_q \log \left[ \frac{p(x_T)\, \displaystyle\prod_{t=1}^{T} p_\theta(x_{t-1} \mid x_t)}{\displaystyle\prod_{t=1}^{T} q(x_t \mid x_{t-1})} \right]$$

Consider

$$\log \left[ \frac{p(x_T)\, \displaystyle\prod_{t=1}^{T} p_\theta(x_{t-1} \mid x_t)}{\displaystyle\prod_{t=1}^{T} q(x_t \mid x_{t-1})} \right]$$

We take out only the first conditional
$$= \log \frac{p(x_T)\, p_\theta(x_0 \mid x_1)\, \displaystyle\prod_{t=2}^{T} p_\theta(x_{t-1} \mid x_t)}{q(x_1 \mid x_0)\, \displaystyle\prod_{t=2}^{T} q(x_t \mid x_{t-1})}$$

$$= \log \frac{p(x_T)\, p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)} + \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_t \mid x_{t-1})}$$
Consider the Denominator in the Second Term

$$q\left(x_t \mid x_{t-1}\right) = q\left(x_t \mid x_{t-1}, x_0\right) \quad \because \text{ 1st order Markov property}$$
Using the [[Bayes Rule]] . In the second term the numerator was denoting the backward process and the denominator was denoting the forward process. What we want to do is denote both the terms such that the represent one direction only. 
$$= \frac{q\left(x_{t-1} \mid x_t, x_0\right) \cdot q\left(x_t \mid x_0\right)}{q\left(x_{t-1} \mid x_0\right)} \quad \text{: Bayes' rule with 3 RVs.}$$

$q\left(x_{t-1} \mid x_t, x_0\right)$ : distribution of $x_{t-1}$, given that the Encoding process has landed at $x_t$ at $t=t$, starting from $x_0$. Can look at this as the "True Reverse distribution"

---

Plugging the above expression on to the ELBO,

$$\log \frac{p(x_T)\; p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)} + \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_t \mid x_{t-1})}$$

$$= \log \frac{p(x_T)\; p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)} + \log \prod_{t=2}^{T} \left( \frac{p_\theta(x_{t-1} \mid x_t)}{\dfrac{q(x_{t-1} \mid x_t, x_0), q(x_t \mid x_0)}{q(x_{t-1} \mid x_0)}} \right)$$

$$= \log \frac{p(x_T)\; p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)}+ \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)\, . q(x_{t-1} \mid x_0)}{q\left(x_{t-1} \mid x_t, x_0\right) \cdot q(x_t \mid x_0)}$$
$$= \log \frac{p(x_T), p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)} + \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)} +$$

$$\left( \log \prod_{t=2}^{T} \frac{q(x_{t-1} \mid x_0)}{q(x_t \mid x_0)} = \log \frac{q(x_1 \mid x_0), q(x_2 \mid x_0)}{q(x_2 \mid x_0), q(x_3 \mid x_0)} \cdots \right)$$

$$= \log \frac{p(x_T)\, p_\theta(x_0 \mid x_1)}{q(x_1 \mid x_0)} + \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)} + \log \frac{q(x_1 \mid x_0)}{q(x_T \mid x_0)}$$
Now the numerator of the third term is cancelled with the denominator of the first term. And the denominator of the third term is now accommodated in the denominator of the second term in the below equation

$$= \log p_\theta(x_0 \mid x_1) + \log \frac{p(x_T)}{q(x_T \mid x_0)} + \log \prod_{t=2}^{T} \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)}$$

$$= \log p_\theta(x_0 \mid x_1) + \log \frac{p(x_T)}{q(x_T \mid x_0)} + \sum_{t=2}^{T} \log \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)}$$

$$\underbrace{\hspace{8cm}}_{\text{Term}}$$

Bringing in the outer expectation term,
$$\mathbb{E}_{q(x_{1:T} \mid x_0)}\left(\text{Term}\right)$$

Since the sub-terms in (Term) depends only on subsets of $x_{1:T}$, the outer expectation can be written appropriately.

$$J_\theta(q) = \mathbb{E}_{q(x_1 \mid x_0)} \log p_\theta(x_0 \mid x_1) + \mathbb{E}_{q(x_T \mid x_0)} \log \frac{p(x_T)}{q(x_T \mid x_0)}$$

$$+ \sum_{t=2}^{T} \mathbb{E}_{q(x_{t-1},\, x_t \mid x_0)} \log \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)}$$

Consider $\mathbb{E}_{(x_{t-1},\, x_t \mid x_0)}\left(\;\right) = \mathbb{E}_{q(x_t \mid x_0)} \cdot \mathbb{E}_{q(x_{t-1} \mid x_t,, x_0)}\left(\;\right)$

The above is a [[Property of the conditional expectation]]

Rewriting the ELBO using the property of cond. exp.

$$\mathbb{E}_{q(x_1 \mid x_0)} \log p_\theta(x_0 \mid x_1) + \mathbb{E}_{q(x_T \mid x_0)} \log \frac{p(x_T)}{q(x_T \mid x_0)}$$

$$+ \sum_{t=2}^{T} \mathbb{E}_{q(x_t \mid x_0)} \cdot \mathbb{E}_{q(x_{t-1} \mid x_t,, x_0)} \left( \log \frac{p_\theta(x_{t-1} \mid x_t)}{q(x_{t-1} \mid x_t, x_0)} \right)$$
The second term is the negative of the KL

$$\boxed{= \mathbb{E}_{q(x_1 \mid x_0)} \log p_\theta(x_0 \mid x_1) - D_{KL}\!\left(q(x_T \mid x_0) ,|, p(x_T)\right) - \sum_{t=2}^{T} \mathbb{E}_{q(x_t \mid x_0)} \left[ D_{KL}\!\left(q(x_{t-1} \mid x_t, x_0) \!||\, p_\theta(x_{t-1} \mid x_t)\right) \right]}$$

---

The above objective of DDPM contain three terms:

**i)** $\mathbb{E}_{q(x_1 \mid x_0)} \log p_\theta(x_0 \mid x_1)$ : Reconstruction term.

**ii)** $D_{KL}\!\left(q(x_T \mid x_0) \,||\, p(x_T)\right)$ : prior matching term — Independent of $\theta$ so we ignore this from now on. No matter what model params you take

**iii)** $\displaystyle\sum_{t=2}^{T} \mathbb{E}_{q(x_t \mid x_0)} \left[ D_{KL}\!\left(\underbrace{q(x_{t-1} \mid x_t, x_0)}_{\text{"Known" denoising}} \,||\, \underbrace{p_\theta(x_{t-1} \mid x_t)}_{\text{learnable denoising}}\right) \right]$ Consistency or Denoising matching term



**Objective:** $\theta^* = \underset{\theta}{\mathrm{argmax}}; J_\theta(q)$ (ELBO)
Find a theta star to maximise the ELBO

---

## Estimating the $D_{KL}$ in the Consistency Term

$$D_{KL}\!\left(q(x_{t-1} \mid x_t, x_0) \,||\, p_\theta(x_{t-1} \mid x_t)\right)$$

#### To Compute the known denoising term $q(x_{t-1} \mid x_t, x_0)$
All the definitions we have are for the forward process so we will invert this again using bayes rule. 
$$q\left(x_{t-1} \mid x_t, x_0\right) = \frac{q\left(x_t \mid x_{t-1}, x_0\right) \cdot q\left(x_{t-1} \mid x_0\right)}{q\left(x_t \mid x_0\right)} \quad \text{Bayes' rule}$$

$$= \frac{q\left(x_t \mid x_{t-1}\right) \cdot q\left(x_{t-1} \mid x_0\right)}{q\left(x_t \mid x_0\right)}$$

We know

$$q\left(x_t \mid x_{t-1}\right) = \mathcal{N}\!\left(x_t;\; \sqrt{\alpha_t}\, x_{t-1},\, (1-\alpha_t)\, I\right)$$
Because we defined the forward process like this.

$q(x_t \mid x_0)$ can be obtained using recursion as below:

We have,

$$x_t = \sqrt{\alpha_t}\cdot x_{t-1} + \sqrt{1-\alpha_t}, \epsilon_{t-1} \qquad \epsilon_{t-1} \sim \mathcal{N}(0, I)$$

$$= \sqrt{\alpha_t}\cdot\left(\sqrt{\alpha_{t-1}}\cdot x_{t-2} + \sqrt{1-\alpha_{t-1}}\cdot \epsilon_{t-2}\right) + \sqrt{1-\alpha_t}\, \epsilon_{t-1}$$

$$\epsilon_{t-2} \sim \mathcal{N}(0, I)$$

$$= \sqrt{\alpha_t \cdot \alpha_{t-1}}\; .  x_{t-2} + \underbrace{\sqrt{\alpha_t - \alpha_t \alpha_{t-1}}\cdot \epsilon_{t-2} + \sqrt{1-\alpha_t}\,. \epsilon_{t-1}}_{T_2}$$

Consider $T_2 = \sqrt{\alpha_t - \alpha_t \alpha_{t-1}}\cdot \epsilon_{t-2} + \sqrt{1-\alpha_t}\, . \epsilon_{t-1}$ Linear combination of two RV's drawn iid from a Isotropic Normal Distribution

$$= a\cdot\epsilon_1 + b\cdot\epsilon_2 \qquad \epsilon_1, \epsilon_2 \sim \text{iid}\; \mathcal{N}(0, I)$$

$T_2$ is a linear combination of two normal RVs & $\therefore$ it'll lead to another Gauss. RV.

$$T_2 = \epsilon^* \sim \mathcal{N}\!\left(0,\, (1 - \alpha_t \cdot \alpha_{t-1})\, . I\right)$$

$$x_t = \sqrt{\alpha_t \cdot \alpha_{t-1}}\; x_{t-2} + \left(\sqrt{1 - \alpha_t \alpha_{t-1}}\right) \epsilon^*_{t-2}$$

continuing the recursion till $x_0$, $\quad \epsilon_{t-2}^* \sim \mathcal{N}(0, I)$ 

$$x_t = \sqrt{\alpha_t \cdot \alpha_{t-1} \cdots \alpha_1}\, x_0 + \sqrt{1 - \alpha_t \alpha_{t-1} \cdots \alpha_1}\cdot \epsilon \qquad \epsilon \sim \mathcal{N}(0, I)$$

$$x_t = \sqrt{\bar{\alpha}_t}\cdot x_0 + \sqrt{1 - \bar{\alpha}_t}\cdot \epsilon$$
X-t is the scaled and shifted version of an isotropic gaussian.
where $\bar{\alpha}_t = \displaystyle\prod_{i=1}^{t} \alpha_i \qquad \epsilon \sim \mathcal{N}(0, I)$

$$q(x_t \mid x_0) = \mathcal{N}\!\left(x_t;\; \sqrt{\bar{\alpha}_t}\cdot x_0,\; (1 - \bar{\alpha}_t)\, I\right)$$

$\Rightarrow$ $t^{\text{th}}$ latent can be obtained directly from the data ($x_0$), without hopping for $t$-steps.

---

Getting back to the Consistency term

$$q(x_{t-1} \mid x_t, x_0) = \frac{q(x_t \mid x_{t-1}) \cdot q(x_{t-1} \mid x_0)}{q(x_t \mid x_0)}$$

$$q\left(x_t \mid x_{t-1}\right) = \mathcal{N}\!\left(x_t;\; \sqrt{\alpha_t}\, x_{t-1},\; (1-\alpha_t)\, I\right)$$

$$q\left(x_t \mid x_0\right) = \mathcal{N}\!\left(x_t;\; \sqrt{\bar{\alpha}_t}\, x_0,\; (1-\bar{\alpha}_t)\, I\right)$$

$$q\left(x_{t-1} \mid x_0\right) = \mathcal{N}\!\left(x_{t-1};\; \sqrt{\bar{\alpha}_{t-1}}\cdot x_0,\; (1-\bar{\alpha}_{t-1})\, I\right)$$
$$\Rightarrow\quad q(x_{t-1} \mid x_t, x_0) \propto \exp\!\left[-\|x_t - (\cdot)\|_2^2\right] \cdot \exp\!\left(-\|x_{t-1} - (\cdot)\|_2^2\right)$$

$$\div\; \exp\!\left[-\|x_{t-1} - (\cdot)\|_2^2\right]$$

TODO : Plug in all the equations for the 3 Multivariate Gaussian distributions and one would get this formulation
$$\propto \exp\!\left[-\|x_{t-1} - \mu_q\|_2^2\right]$$

obtained via [[Completion of the Square method]]
Mean is a function of $x_t$ and $x_o$ because of course those are the [[conditioning variables]] 
$$q\left(x_{t-1} \mid x_t, x_0\right) = \mathcal{N}\!\left(x_{t-1};\; \mu_q(x_t, x_0),\; \Sigma_q\right)$$

where,
TODO : Derive the below . Alphas are all scalars they are scaling the vector x_t element-wise

$$\mu_q(x_t, x_0) = \frac{\sqrt{\alpha_t}\,(1-\bar{\alpha}_{t-1})\cdot x_t + \sqrt{\bar{\alpha}_{t-1}}\,(1-\alpha_t)\cdot x_0}{1 - \bar{\alpha}_t}$$

$$\Sigma_q = \frac{(1-\alpha_t)(1-\bar{\alpha}_{t-1})}{1-\bar{\alpha}_t} \cdot I$$

$$= \sigma_q^2 \cdot I$$

Both $\mu_q$ & $\Sigma_q$ and $\therefore$

$q(x_{t-1} \mid x_t, x_0)$ are computable & known.

$$D_{KL}\!\left(q(x_{t-1} \mid x_t, x_0) \,\|\, p_\theta(x_{t-1} \mid x_t)\right)$$

$$p_\theta(x_{t-1} \mid x_t) = \mathcal{N}(x_{t-1};\; \mu_\theta,\; \Sigma_q)$$
In practice what is done is , only the mean is computed and variance is kept the same as that of q. this is a design choice. 
$$\Rightarrow\quad D_{KL}\!\left(q(x_{t-1} \mid x_t, x_0) \,\|\, p_\theta(x_{t-1} \mid x_t)\right)$$

$$= D_{KL}\!\left[\mathcal{N}(x_{t-1};\; \mu_q, \Sigma_q) \,\|\, \mathcal{N}(x_{t-1};\; \mu_\theta, \Sigma_q)\right]$$
$\mu_{\theta}$ is the only term that needs to be computed.
[[KL divergence between two Gaussians]] is known. 
$$= \frac{1}{2}\left[\log \frac{|\Sigma_q|}{|\Sigma_q|} - d + \mathrm{tr}\!\left(\Sigma_q^{-1}\Sigma_q\right) + (\mu_\theta - \mu_q)^T \Sigma_q^{-1}(\mu_q - \mu_\theta)\right]$$
$$\underbrace{\hspace{2cm}}_{I}$$
The mu's are d dimensional vectors because they are the means of a d-dimensional Gaussian distribution
The first term is log of 1 which is 0. the minus d and the trace value cancel each other out as the matrix inside the trace function is and Identity matrix and
$$\Sigma_q^{-1} = (\sigma_q^2\, I)^{-1}$$

$$= \frac{1}{2\sigma_q^2} \left\|\mu_\theta - \mu_q\right\|_2^2 \quad \text{: Regression over } \mu_q$$
This is the squared error cost. 
