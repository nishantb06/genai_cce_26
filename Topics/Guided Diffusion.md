# Guided Diffusion Models for Conditional Generation

Data : $(x_0, y)$ where $y$ : conditioning variable

E.g. $x_0$ : Image $\quad y$ : Class-label / text Embedding


**Goal:** sample from the conditional distribution $p(x_0 \mid y)$?

**Question:** How to modify a DDPM to sample from the cond. dist. $p(x_0 \mid y)$?
##### Classifier Guidance

Recall that DDPMs are score-predictors, predicting the true score of the unconditional or marginal distribution, $\nabla_{x_t} \log p(x_t)$

From a conditional sampling perspective, the goal is to predict or regress over the conditional [[Score function|score]], $\nabla_{x_t} \log p(x_t \mid y)$

$$\nabla_{x_t} \log p(x_t \mid y) = \nabla \log \left(\frac{p(x_t)\cdot p(y \mid x_t)}{p(y)}\right)$$

$$= \nabla_{x_t} \log p(x_t) + \nabla_{x_t} \log p(y \mid x_t) - \cancel{\nabla_{x_t} \log p(y)}$$

$$\boxed{\nabla_{x_t} \log p(x_t \mid y) = \nabla_{x_t} \log p(x_t) + \nabla_{x_t} \log p(y \mid x_t)}$$

$$\quad \quad \quad \quad \quad \quad \underbrace{\hspace{2.5cm}}_{\text{unconditional score}} \qquad \underbrace{\hspace{2.5cm}}_{\text{classifier gradient}}$$
The  second term cannot be called a score

---

## Diagram

$$y,\; x_{t}, t \rightarrow \underbrace{\text{U-net}}_{\substack{\text{decrease} \ \text{dim}};\theta;\substack{\text{increase} \ \text{dim}}} \rightarrow |\epsilon_t - \hat{\epsilon}_\theta|_2^2 \xrightarrow{\text{predict unconditional score}} \hat{\epsilon}_\theta ;\left(\nabla_{x_t} \log p(x_t)\right)$$

$$\nabla_\theta |\epsilon_t - \hat{\epsilon}_\theta|_2^2 + \nabla_{x_t} \log p(y \mid x_t)$$
Train a classifier or a regressor separately
$$x_t \rightarrow \underbrace{\text{Classifier / Regression}}_{\text{pre trained}} \rightarrow p(y \mid x_t) \xrightarrow{} \nabla_{x_t} \log p(y \mid x_t)$$

Classifier / Regressor is trained separately to predict $y$ (class label or Embedding) from $x_t$.

This neural network is trained before training the DDPM model. As one can take the gradients wrt the labels , we can also take the gradients wrt the inputs. This is what we need to do here . This classifier is not used during inference at all

Training the classifier at different noise levels is difficult. Irrespective of the noise levels we are expecting to predict the class as cat . That is difficult to do 

Which is why another method called [[Classifier Free Guidance]]

