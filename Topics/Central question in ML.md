
> **Given observations (elements from the range space of $X$), what is the underlying distribution?**

### Dataset

$$\mathcal{D} = \{x_1, x_2, \ldots, x_N\} \overset{\text{iid}}{\sim} P_X$$

**iid** =[[ Independent and Identically Distributed]]:

$$P(A_1 \cap A_2) = P(A_1) \cdot P(A_2)$$

## 5. Problems in Machine Learning

### Dataset Structure

$$\mathcal{D} = \{(x_i, y_i)\}_{i=1}^{N} \overset{\text{iid}}{\sim} P_{XY}$$

### a) Supervised Learning :
Estimate the [[Conditional Probability Distribution]]

- **Classification:** $y \in \{1, 2, \ldots, K\}$ — estimate $P_{Y|X}$
- **Regression:** $y \in \mathbb{R}^m$ — estimate $P_{Y|X}$
  - Example use cases: bounding box extraction, supervised segmentation

$$X \in \mathbb{R}^d \xrightarrow{P_{Y|X}} \text{seg. / label}$$

### b) Unsupervised Learning — Estimating Marginals

- Knowing the distribution of image pixels ($P_X$)
- Knowing the distribution of occurrence of a label in a population ($P_Y$)
- 
## 6. Generative Modelling

> **Given** $\mathcal{D} = \{x_i\}$, **estimate** $P_X$ **and sample from it.**

The Sample from it is the most important part ! 

Two modes:

| Mode | Description |
|------|-------------|
| Unconditional generation | Simulate $P_X$ — reproduce the underlying random experiment |
| Conditional generation | Sample from $P_{X \mid Y}$ |
