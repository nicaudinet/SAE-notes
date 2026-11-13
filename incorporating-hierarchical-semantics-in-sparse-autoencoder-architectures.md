---
tags:
  - paper
---
https://arxiv.org/pdf/2506.01197v1

Paper by [Victor Veitch](./people/Victor%20Veitch.md) and others.

---

They propose a hierarchical [[mixture-of-experts]]-style architecture for [SAEs](./SAE-sparse-autoencoders.md). They argue that this allows them to learn hierarchical features more efficiently, which in turn mitigates problems like [feature splitting](./feature-splitting-in-sparse-autoencoders.md).

They use [TopK](./topk-sparse-autoencoders.md) SAEs with LeakyReLU:
$$
\begin{align}
f(\textbf{x}) & = \text{TopK}_k (\text{LeakyReLU}_\alpha(\textbf{E}(\textbf{x} - \textbf{b}))) \\
\text{SAE}_k(\textbf{x}) & = \textbf{D}f(\textbf{x})
\end{align}
$$
and train them with the MSE reconstruction loss:
$$
\mathcal{L}_\text{recon} = \| \textbf{x} - \text{SAE}_k(\textbf{x}) \| ^2_2
$$

# Hierarchical SAE architecture

They train a relatively small high-level SAE which identifies whether a concept is active or not (e.g. "dog" vs. "not dog") and then, for each feature in the high-level SAE, they train a low-level SAE which distinguishes between the categories in that concept (e.g. "corgi", "greyhound", etc.).

In practice it looks like this:
$$
\text{H-SAE}(\textbf{x}) =
\sum_{j \in \text{TopKIndices}_k}
(
\underbrace{z_j \textbf{d}_j}_{\hat{\textbf{x}} ^\text{high}}
+
\underbrace{
\Pi^\text{up}_j \text{SAE}^1_j (\Pi^\text{down}_j \textbf{x})
}_{\hat{\textbf{x}}^\text{low}_j}
)
$$
where
- $\textbf{d}_j$ is feature $j$ in the high-level SAE
- $z_j = (\text{LeakyReLU}(\textbf{Ex}))_j$ is the activation for feature $\textbf{d}_j$
- $\Pi^\text{up}_j$ and $\Pi^\text{down}_j$ are projection matrices of size $s$
- $\text{SAE}^1_j$ is the low-level SAE for high-level feature $j$
- $\text{TopKIndices}_k$ are the indices of the top $k$ high-level features

The training objective is given by:
$$
\mathcal{L} = \mathcal{L}_\text{recon} + \lambda_1 \mathcal{L}_\text{ortho} + \lambda_2 \mathcal{L}_\text{sparse}
$$

The reconstruction loss penalises both the final reconstruction loss and just the reconstruction from the high-level features to encourage them to be meaningful:
$$
\mathcal{L}_\text{recon} =
\| \textbf{x} - \text{H-SAE}(\textbf{x}) \| ^2_2b
+ \beta
\| \textbf{x} - \hat{\textbf{x}}^\text{high} \| ^2_2
$$

They use an orthogonality loss term on the high-level features to discourage feature duplication and instead encourage feature compositionality:
$$
\mathcal{L}_\text{ortho} = \frac{
\| \textbf{ED} - \text{diag}(\textbf{ED}) \|_F
}{
m^2_\text{top} - m_\text{top}
}
$$
They are unsure if this actually achieves their goals, but observe that it seems to work empirically.

They also include a small L1 sparsity loss term on feature activations for both the high-level SAE and the low-level SAEs additional to the TopK constraint.