Given a true distribution $P_X$ with density $p_X(x)$ and a model $P_\theta$ with density $p_\theta(x)$:

$$\int_{\mathcal{X}} p_X(x)\, dx = 1 \quad \text{(valid probability measure)}$$

> Note: $p_\theta(x)$ is the *[[Likelihood|likelihood]]* of $x$ under $\theta$, not necessarily a probability measure by itself.

In the example where we flip a fair coin twice, the pmf is

pX(0) = P[{(T,T)}] = 1/4
pX(1) = P[{(T,H),(H,T)}] = 2/4 ,
and pX(2) = P[{(H,H)}] = 1/4 ,

Note that this satisfies the above discretized version of the integral. 

The pmf can be represented by a histogram, or some parametric function (see Section 2.2.1). We call pX the probability distribution for the [[Random Variables]] X

The corresponding Cumulative density function would be 
pX(x<=0) = 1/4
pX(x<=1) = 3/4
pX(x<=2) = 1

