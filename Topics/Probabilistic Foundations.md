[[Probability is a measure of the size or weight or volume of a set]]
### Recap on Probability Theory

**Motivation:** We model uncertainty via repeated observations.

**Example — Automatic Speech Recognition (ASR):**
- Signal $x(t)$ is a time-series pressure measurement, converted to voltage via a microphone.
- A linear system maps $x(t) \to \{\hat{a}, \hat{e}, \hat{i}, \hat{o}, \ldots\}$ (phonemes).
- This is a transition from a *physical measurement* (pressure, differential, integral) to a *semantic abstraction* (phonemes, shapes).

### Probability Space $(\Omega, \mathcal{F}, P)$ 
This triplet is the core of all the probability related conversations we have. 

| Symbol        | Name                    | Description                                         |
| ------------- | ----------------------- | --------------------------------------------------- |
| $\Omega$      | [[Sample space]]        | Set of all possible outcomes of a random experiment |
| $\mathcal{F}$ | [[Event space]]         | Set of all subsets of $\Omega$ (sigma-algebra)      |
| $P$           | [[Probability measure]] | $P: \mathcal{F} \to \mathbb{R}^+$                   |

Related
[[Lebesgue Measure]]
[[Conditional Probability Distribution]]
[[Marginal Distribution]]
[[Joint Distribution]]
[[Probability Density]]
