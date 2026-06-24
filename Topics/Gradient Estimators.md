[[Gradient Variance]] is something you need to care about, of course it shouldn't be too high
There are different Gradient estimators , applicable in different scenario's and all have different variances. For example [[Monte Carlo Gradient Estimators]] . Survey [paper](https://arxiv.org/pdf/1906.10652) on MC gradient estimators in ML
There are two that you should care about 

- [[Reinforce estimator]] (score function): very general purpose, large variance
- [[Reparameterization Trick | Reparameterisation]]  ( path derivative): less general purpose, much smaller variance.