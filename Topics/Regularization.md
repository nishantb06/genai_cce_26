Imposing certain restrictions on the parameter distribution or the activation distribution, usually a term added to the base loss function

$$L_\theta(\cdot) + \lambda \cdot \Omega(\theta)$$

$$\underbrace{\hspace{1.5cm}}_{\text{Cost fn}} \qquad \underbrace{\hspace{1.5cm}}_{\substack{\text{regularization fn} \ \text{reg const} \rightarrow}}$$

--- 
From [[Bias Variance Decomposition]]
Any methods which increase the bias of the model is called regularisation.

--- 
Different Regularisation techniques

[[Early stopping]]
[[Batch Normalisation]]
[[Layer Normalisation]]


1. Parameter penalty: Restrict the values the parameters can take
Parameter penalty is now a Constrained optimization problem. 
$$\left.
\begin{aligned}
\underset{\theta}{\mathrm{argmin}} \; D\left(P_x \,\middle|\, P_\theta\right) \\
\text{s.t.} \quad \Omega(\theta) &< K
\end{aligned}
\right\} \text{will lead to a model with higher bias.}$$

Any [[Constrained Optimization problem]] is solved using a [[Lagrangian]]

2.  Penalty on the latent variable models
Output of each layer can be thought of as a latent variable
X -> z1 ->z2 ->z3 -> ..... -> X_hat

we can penalise z_i's as well by adding a penalty term in the loss function
Because this is indirectly a penalty on the model weights. 

[[A model can be regularised by penalising the values of the latent variables]]
All such methods which do this are called Normalisation like [[Batch Normalisation]] and [[Layer Normalisation]] etc. 

3. Architectural Modifications
[[Dropout | Restricting the connection of one neuron to others]] is a very strong regulariser, because we are restricting weights to zero. 

With this idea in mind [[CNN's]] are [[CNN's are regularised MLP's | Regularised MLP's]]
All architecture innovations are forms of regularisation. Regularisation introduces bias. What kind of bias is good bias for a particular problem statement is the main question. 


