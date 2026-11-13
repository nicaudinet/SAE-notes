---
tags:
  - notes/paper
---
https://arxiv.org/pdf/2412.06410

---

An extension of [TopK SAEs](./topk-sparse-autoencoders.md). Rather than taking the top k for each sample it relaxes the constraint to the batch level during training. Rather than retaining the top $k$ activations in each sample, you instead rank activations for the whole batch and retain the top $bk$ activations where $b$ is the batch size. $k$ becomes the average sparsity level in the batch.

Some samples may require more features for accurate reconstruction than others. BatchTopK allows for a variable number of active features per sample within the batch, improving reconstruction without affecting average sparsity.

The SAE structure remains very close to a TopK SAE: 
$$
\begin{align}
\textbf h &= \text{ReLU}(W_\text{enc} \textbf x + \textbf b_\text{enc})\\
\textbf z &= \text{BatchTopK}_{Bk}(h) \\
\hat{\textbf x} &= W_\text{dec} \textbf z + b_\text{dec}
\end{align}
$$

and the training objective becomes:
$$
\mathcal{L} = \frac{1}{B} \sum_{i=1}^B \| \textbf x_i - \hat{\textbf x_i} \|^2_2
$$

At inference time a one approach is to replace BatchTopK with a fixed activation threshold $\tau$ learned calibrated with training activations:
$$
\textbf z_i = h_i \mathbb{1}[h_1 > \tau]
$$