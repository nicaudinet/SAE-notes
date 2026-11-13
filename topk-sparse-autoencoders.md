---
title: TopK SAEs
---
An [SAE](./SAE-sparse-autoencoders.md) variant [developed by OpenAI researchers](./scaling-and-evaluating-sparse-autoencoders.md) aimed to prevent [feature collapse](./feature-collapse-in-sparse-autoencoders.md).

Rather than penalising feature activation in the loss TopK SAEs explicitly limit the number of active features. They do this with a $\text{TopK} : \R^n \to \R^n$ function that keeps the $k$ largest latents and zeros out the rest:
$$
\begin{align}
\textbf z &= \text{TopK}(\text{ReLU}(W_\text{enc}(\textbf x - b_\text{pre}))) \\
\hat{\textbf x} &= W_\text{dec} \textbf z + b_\text{dec}
\end{align}
$$

They are only trained on the reconstruction loss as the sparsity is encoded in the structure:
$$
\mathcal{L} = \| \textbf x - \hat{\textbf x} \|^2_2
$$

Empirically, having only $k$ features can be active at any one time penalises redundant features and encourages feature splitting more directly.

TopK SAEs struggle with [dead neurons](./dead-neurons-in-sparse-autoencoders.md) more than vanilla SAEs.