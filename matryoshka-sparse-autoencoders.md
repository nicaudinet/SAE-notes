---
title: Matryoshka SAEs
---
Matryoshka SAEs learns nested SAEs of different sizes simultaneously with only a modest increase in training time (depending on the nesting number).

They are designed to mitigate feature [splitting](./feature-splitting-in-sparse-autoencoders.md), [absorption](./feature-absorption-in-sparse-autoencoders.md) and [composition](./feature-composition-in-sparse-autoencoders.md). They show that this architecture mitigates absorption and improves performance on concept erasure tasks like [SHIFT](./SHIFT-sparse-human-interpretable-feature-trimming.md).

Given a maximum dictionary size $m$ define a sequence of $n$ nested sizes
$$
\mathcal{M} = m_1, m_2, \ldots, m_n,  \qquad m_1 < m_2 < \ldots < m_n = m
$$
You can either sample $\mathcal{M}$ randomly per batch or set $\mathcal{M}$ as a hyper-parameter before training.

The encoder is defined as before, for example using [BatchTopK](./BatchTopK-sparse-autoencoders.md):
$$
\textbf z = \text{BatchTopK}_{Bk}(\text{ReLU}(W_\text{enc} \textbf x + \textbf b_\text{enc} ))
$$
However, now we reconstruct using progressively larger sizes of $m$:
$$
\begin{align}
\hat{\textbf x}_{1} &= W_\text{dec}^{0:m_1} \textbf{z}_{0:m_1} + \textbf b_\text{dec} \\
\hat{\textbf x}_{2} &= W_\text{dec}^{0:m_2} \textbf{z}_{0:m_2} + \textbf b_\text{dec} \\
&\ldots \\
\hat{\textbf x}_{n} &= W_\text{dec}^{0:m_n} \textbf{z}_{0:m_n} + \textbf b_\text{dec} \\
\end{align}
$$

The loss function then minimises the sum of the reconstructed losses:
$$
\mathcal{L} = \sum_{m \in \mathcal{M}} \alpha_m \| \textbf x - \hat{\textbf x}_m \|^2_2
$$
where $\alpha_m$ controls the relative importance of each reconstruction. There is no sparsity term since we are using BatchTopK SAEs as a base.

In this way, early features contribute to many training objectives while later features only contribute to a few. Early features are therefore encouraged to represent more general concepts, while later features are encouraged to specialise.

At inference you just pick an $m \in \mathcal{M}$ (often the full dictionary) based on what level of granularity you prefer.

Matryoshka SAEs are used in GemmaScope 2.