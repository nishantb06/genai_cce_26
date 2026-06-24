
This is commonly used in Reinforcement Learning. It is named score function because it utilises this “cool little logarithm trick”:

$$
\nabla_\theta \log p(x,\theta)
=
\frac{\nabla_\theta p(x;\theta)}{p(x;\theta)}
$$

So now, when we try to estimate the gradient of some function \(f(x)\) under the expectation of distribution $p(x,\theta)$ , we can do the following:

$$
\nabla_\theta \mathbb{E}_{x\sim p(x,\theta)}[f(x)]
=
\mathbb{E}_{x\sim p(x,\theta)}
\left[
f(x)\nabla_\theta \log p(x,\theta)
\right]
$$

and now we can easily estimate the gradient by performing MC sampling — taking N samples of $\hat{x}\sim p(x,\theta)$:

$$
\nabla_\theta \mathbb{E}_{x\sim p(x,\theta)}[f(x)]
\approx
\frac{1}{N}
\sum_{n=1}^{N}
f(\hat{x}^{(n)})
\nabla_\theta
\log p(\hat{x}^{(n)};\theta)
\, .
$$

Keep in mind that this score function estimator estimator, despite being unbiased, has very large variance from multiple sources (see here in section 4.3.1 for details). It is however very flexible and places no requirement on $p(x;\theta)$ or $f(x)$ — hence its popularity


---
My take : 
The derivative of a log is called the [[Score function]] and it usually has a very high variance . Even when you write down the equations of the derivative of the [[Evidence Lower Bound | ELBO]] a score function term will appear which causes the gradient of ELBO to have a high variance, even though we used reparameterisation initially which is know to have a lower variance. 



