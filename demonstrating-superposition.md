---
title: Demonstrating superposition
---
The "Demonstrating Superposition" experiment from the [Toy Models of Superposition](./toy-models-of-superposition.md) blog post.

Can a simple neural network can project some high-dimensional $x \in \R^n$ into a  lower-dimensional $h \in \R^m$ and recover it?

Each $x_i$ corresponds to a feature (since it is what we would expect in the hypothetical disentangled model according to the linear representation hypothesis). Each $x_i$ has as corresponding sparsity $S_i$ and importance $I_i$. $x_i = 0$ with probability $S_i$ else it is uniformly sampled from $[0,1]$. This balances:
- Feature sparsity (features typically occur rarely in the wild)
- More features than neurons (can have as many $x_i$s as we want)
- Features of varying importance (importance score)

Linear model:
$$
\begin{align}
h &= Wx \\
x' & = W^T h + b = W^T W x + b
\end{align}
$$

ReLU Output model:
$$
\begin{align}
h &= Wx \\
x' & = ReLU( W^T h + b) = ReLU (W^T W x + b)
\end{align}
$$

$W \in \R^{m \times n}$, and each column represents the direction in $\R^m$ for feature $x_i$.

The loss is the MSE weighted by the feature importance:
$$
L = \sum_x \sum_i I_i(x_i - x_i')^2
$$

They show in the experiment that for $n = 20$ and $m = 5$ the linear model only learns the 5 principal components. The $ReLU$ model, however, starts learning more entangled features as sparsity increases.

In their analysis they explain that the $ReLU$ model is balancing:
- Feature Benefit - the value the model gets by representing a feature
- Interference - the noise from non-orthogonal features

Result by Saxe for the linear case:
$$
L \sim \sum_i I_i( 1 - \| W_i \|^2)^2 + \sum_{i \neq j} I_j (W_j \cdot W_i)^2
$$

They relate this to the Thompson Problem in chemistry which has to do with packing points on a sphere.