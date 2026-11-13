---
tags:
  - notes/paper
---
https://arxiv.org/abs/2407.14435

---

JumpReLU SAEs swap the ReLU function in baseline [SAEs](./SAE-sparse-autoencoders.md) for a JumpReLU function which zeros out all activations below a certain threshold:
$$
\text{JumpReLU}_\theta(h) :=
\begin{cases}
0 & h \leq \theta \\
h & h > \theta
\end{cases}
$$

The parameter $\theta > 0$ specifies a threshold for each feature for which the feature is considered active. This separates the tasks of determining which features are active from determining the magnitude of the active features, mitigating [feature shrinkage](./feature-shrinkage-in-sparse-autoencoders.md).

The JumpReLU SAE architecture is:
$$
\begin{align}
\textbf h &= W_\text{enc} \textbf x + \textbf b_\text{enc} \\
\textbf z &= \text{JumpReLU}_\Theta(\textbf h) \\
\hat{\textbf x} &= W_\text{dec} \textbf z + b_\text{dec}
\end{align}
$$

In other words, each feature $i$ has its own learned threshold $\theta_i > 0$:
$$
z_i = h_i \mathbb{1}[h_i > \theta_i]
$$

The usual training objective is a reconstruction loss and $L0$ sparsity penalty:
$$
\mathcal{L} = \| \textbf x - \hat{\textbf{x}} \|^2_2 + \lambda \| \textbf z \|_0
$$

The difficulty is that the usual loss function with JumpReLU doesn't provide gradient signal that can be used for training the SAE. Instead, they use [straight-through-estimators](./estimating-or-propagating-gradients-through-stochastic-neurons-for-conditional-computation-straight-through-estimators.md) and create a pseudo-derivative.