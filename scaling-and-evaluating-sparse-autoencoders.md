---
tags:
  - paper
---
https://arxiv.org/pdf/2406.04093

---

# Baseline

ReLU autoencoders
$$
\begin{align}
z &= \text{ReLU}(W_\text{enc}(x - b_\text{pre}) + b_\text{enc}) \\
\hat x &= W_\text{dec} ~z + b_\text{dec}
\end{align}
$$
with training loss
$$
\mathcal{L} = \|x - \hat x \|^2_2 + \lambda \| z \|_1
$$

# TopK activation function

$k$-sparse autoencoder
$$
\begin{align}
z &= \text{TopK}(W_\text{enc}(x - b_\text{pre})) \\
\hat x &= W_\text{dec} ~z + b_\text{dec}
\end{align}
$$
with training loss
$$
\mathcal{L} = \|x - \hat x \|^2_2
$$

The TopK function only keeps the $k$ largest latents and zeros out the rest which removes the need for the [$L_1$ sparsity penalty](./vector-norms.md) in the loss.