---
title: Toy Models of Superposition
tags:
  - blog
---
https://transformer-circuits.pub/2022/toy_model/index.html

---

Individual neurons don't always map to interpretable features.

In certain cases, models can perform computation while in superposition.

Hypothesis: neural networks are noisily simulating larger, highly sparse networks

[linear-representation-hypothesis](./linear-representation-hypothesis.md)

Why are individual neurons interpretable sometimes? Their hypothesis:
* [Privileged bases](./privileged-basis.md) - not all networks with privileged bases will have basis-aligned features (interpretable neurons), but they are a precondition for it to happen
* Superposition

Working definitions for "feature". They choose the third but are not overly attached to it.
- Feature as any function of the input. Too general
- Feature as properties understandable to humans. What about features we don't understand?
- Features as properties of the input that a sufficiently large model will dedicate a neuron towards representing

The [Superposition Hypothesis](./superposition-hypothesis.md).
# Superposition as a Phase Change

Three outcomes for a feature:
1) The feature may not be learned
2) The feature is learned in superposition with other features
3) The feature is learned with a dedicated dimension

They show that, for a super simple model with $n=2$ and $m=1$, there are clear phase boundaries between varying the sparsity and relative feature importance.  

# The Geometry of Superposition

## Uniform Superposition

Uniform features are independent and have equal sparsity and importance.

They use the Frobenius norm $\|W\|_F^2$ as an indicator for "the number of features learned" since $\|W_i\|^2 \approx 1$ is the feature is represented and $\|W_i\|^2 \approx 0$ if the feature is not. They plot $D^* = \frac{m}{\|W\|_F^2}$ as a measure of "dimensions per feature".

They notice a "sticky point" around $D^* = 1$ and $D^* = 0.5$. They claim this is because the feature directions organise themselves in efficient antipodal pairs where two features are encoded as opposites within a single dimension.

Dimensionality of feature $i$ defined as
$$
D_i = \frac{\|W_i\|^2}{\sum_j(\hat{W_i} \cdot W_j)^2}
$$
where $\hat{W_i}$ is the normalised (unit) version of $W_i$. Roughly "how much feature $i$ is represented" divided by "how many other features share the same dimension".

They observe that features like to organise in particular weight geometries, such as
- Antipodal pairs: 2 features in 1 dimension
- Triangles: 3 features in 2 dimensions
- Tetrahedrons: 4 features in 3 dimensions
- ...

Polytopes.

From this they conclude that there are many types of superposition.

Connection between polytopes and symmetric, positive-definite, low-rank matrices (matrices of the form $W^TW$).

## Non-Uniform Superposition

Features varying in importance deform the polytopes up until a breaking point where they snap to another polytope.

Correlated features prefer to be orthogonal. Anti-correlated features prefer to be opposite. There's some hints of local orthogonality, and a tradeoff between PCA and superposition where, as features become more correlated, PCA becomes better.

# Superposition and Learning Dynamics
Discrete "energy level" jumps. As the networks train, the dimensionality of the features seems to jump to various energy levels as the features organise themselves into polytope configurations.

In some cases, learning can be understood as a sequence of simple, independent geometric transformations.

# Superposition in a Privileged Basis

# Computation in Superposition
Hypothesis: networks can perform computation entirely in superposition rather than just using it to store more features than neurons. 
