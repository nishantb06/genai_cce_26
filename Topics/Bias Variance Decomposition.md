$$\theta^* = \underset{\theta}{\mathrm{argmin}} ; D\left(P_x ,|, P_\theta\right)$$

$$= \underset{\theta}{\mathrm{argmin}} ; -\mathbb{E}_{P_x} \log p_\theta(x)$$

$$\approx \underset{\theta}{\mathrm{argmax}} ; \frac{1}{N} \sum_{i=1}^{N} \log p_\theta(x_i)$$

$$x_i \overset{\text{iid}}{\sim} P_x$$
---

$$D\left(P_x ,|, P_\theta\right) = \text{Bias} + \text{Variance}$$

- **Bias** $\leftarrow$ How close is the model to the true distribution. Quantified with the given data
- **Variance** $\downarrow$ How sensitive is the model to changes in dataset.

We want both bias and variance to be low in an ideal world.
Practically, with less sample , less N

[[Training data]] and [[Test data]] are two samples drawn from the same underlying distribution. 

So if the model has low training error and high test error then the variance is high between samples of the same underlying distribution.

If the model has low training error then the bias is also low.  ONLY for that sample of the underlying distribution !

Bias high variance low -> Underfitting
Bias low Variance high -> Overfitting

Imagine a model which is  $Ax^2 + \epsilon$  where epsilon is gaussian noise
Image two models 
1. $y = y_i$
2. $y = 2$

The first model has 0 bias and extremely high variance. 
The second model has high bias and 0 Variance

--- 

In practice
Start with an over parameterised model and increase its Bias. 
Any methods which increase the bias of the model is called [[Regularization]]

Start with and overtrained model and then ship the model with the least validation accuracy using [[Early stopping]]

[[Validation Data]] is what is used to to tweak the hyperparameters
The moment you touch [[Test data]] you cannot go back and tweak the model hyperparameter and change it. Because then it would be called indirect [[Test data leakage]] .






