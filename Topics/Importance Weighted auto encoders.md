Paper : https://arxiv.org/pdf/1509.00519.pdf (Orignal)
Reinterpreting IWAE : https://arxiv.org/pdf/1704.02916v2
Blog : https://akosiorek.github.io/what_is_wrong_with_vaes/
## Derivation

IWAE proposes a tighter estimate to $\log(p(x))$ . As a reference, here’s the original ELBO again:
$$  
\mathcal{L}(\theta, \phi)  
=  
\mathbb{E}_{z\sim q(z\mid x)}  
\left[  
\log \frac{p(x,z)}{q(z\mid x)}  
\right]  
\leq  
\log p(x)  
$$
A common practice to acquire a better estimate to  with ELBO is to use its multisample variations, by taking  samples from :
$$  
\mathcal{L}_{\text{VAE}}(\theta, \phi)  
=  
\mathbb{E}_{z_1, z_2, \cdots, z_K \sim q(z\mid x)}  
\left[  
\frac{1}{K}  
\sum_{k=1}^K  
\log \frac{p(x,z_k)}{q(z_k\mid x)}  
\right]  
\leq  
\log p(x)  
$$

IWAE simply switch the position between the sum over  and the  of the above, giving us:
$$  
\mathcal{L}_{\text{IWAE}}(\theta, \phi)  
=  
\mathbb{E}_{z_1, z_2, \cdots, z_K \sim q(z\mid x)}  
\left[  
\log  
\frac{1}{K}  
\sum_{k=1}^K  
\frac{p(x,z_k)}{q(z_k\mid x)}  
\right]  
\leq  
\log p(x)  
$$

### Benefit 1: Tighter lower bound estimate
It is easy to see that by [Jensen’s inequality](https://www.probabilitycourse.com/chapter6/6_2_5_jensen's_inequality.php), . This means that IWAE is a tighter lower bound to the marginal log likelihood. $$
\mathcal{L}_{\text{VAE}}(\theta, \phi)
\leq
\mathcal{L}_{\text{IWAE}}(\theta, \phi)
$$

### Benefit 2: Importance-weighted gradients
$$
\begin{align*}
\nabla_\Theta \mathcal{L}_{\text{VAE}}(\theta,\phi)
&=
\mathbb{E}_{z_1, z_2, \cdots, z_K \sim q(z\mid x)}
\left[
\sum_{k=1}^K \frac{1}{K}
\nabla_\Theta
\log \frac{p(x,z_k)}{q(z_k\mid x)}
\right]
\\
\nabla_\Theta \mathcal{L}_{\text{IWAE}}(\theta,\phi)
&=
\mathbb{E}_{z_1, z_2, \cdots, z_K \sim q(z\mid x)}
\left[
\sum_{k=1}^K w_k
\nabla_\Theta
\log \frac{p(x,z_k)}{q(z_k\mid x)}
\right]
\end{align*}
$$
So we can see that in the  the gradients of each samples are **equally weighted** by , but in  gradient weights them by their **relative importance** .

### Benefit 3: Complex implicit distribution
However, this is not all of it — authors in the [original paper](https://arxiv.org/pdf/1509.00519.pdf) also showed that IWAE can be interpreted as standard ELBO, but with a more complex (implicit) posterior distribution , thanks to importance sampling. This is probably the most important take-away of IWAE, and I always like go back to this plot from [reinterpreting IWAE](https://arxiv.org/pdf/1704.02916v2.pdf) as an intuitive demonstration of its power: ![](https://i.imgur.com/pfDciJ7.png) Here, K is the number of importance-weighted samples taken, and the left-most plot is the true distribution that we are trying to approximate with the 3 different . We can see that when , the IWAE objective reduces to original VAE ELBO, and the approximation to true distribution is poor; as K grows, the approximation becomes more and more accurate.


