---
tags:
  - notes/paper
---
https://arxiv.org/pdf/2503.17547

---

Selecting SAE size is tricky: the more features, the more the SAE is incentivised to split or absorb high-level features into more specialised features. 

Sparsity is only an imperfect proxy for interpretability (see [here](./SAE-failure-modes.md)). They mention feature [splitting](./feature-splitting-in-sparse-autoencoders.md), [absorption](./feature-absorption-in-sparse-autoencoders.md) and [composition](./feature-composition-in-sparse-autoencoders.md) as challenges in vanilla SAE training.

To mitigate these problems they propose a new architecture, [Matryoska-SAEs](./matryoshka-sparse-autoencoders.md) that learns nested SAEs of different sizes simultaneously. This should prevent more specific features from taking the role of more general ones. It comes with only a modest increase in training time (depending on the nesting number).

They show that this architecture mitigates absorption and improves performance on concept erasure tasks like [SHIFT](./SHIFT-sparse-human-interpretable-feature-trimming.md).

# Matryoshka SAEs

Given a maximum dictionary size $m$ define a sequence of $n$ nested sizes $\mathcal{M} = m_1, m_2, \ldots, m_n$ where $m_1 < m_2 < \ldots < m_n = m$.
- Random prefix: sample $\mathcal{M}$ randomly per batch
- Fixed prefix: set $\mathcal{M}$ as a hyper-parameter before training

The encoder is defined as normal:
$$
f(x) = \sigma(W^\text{enc} x + b^\text{enc}) \\
$$
where $\sigma$ is the [BatchTopK](./BatchTopK-sparse-autoencoders.md) activation function.

For $m_i \in \mathcal{M}$, the decoders are then defined as:
$$
\begin{align}
\hat x_i (f) & = W^\text{dec}_{0:m_i} f_{0:m_i} + b^\text{dec}
\end{align}
$$

The loss function is defined as:
$$
\mathcal{L} = \sum_{m \in \mathcal{M}} \| x - (f_{0:m} W^\text{dec}_{0:m} + b^\text{dec}) \|^2_2 + \alpha \mathcal{L}_\text{aux}
$$
where
- there is a loss term for each nested SAE
- there is an aux term (same as from [scaling-and-evaluating-sparse-autoencoders](./scaling-and-evaluating-sparse-autoencoders.md))
- there is no sparsity term

# Experiments

They first train a toy model to demonstrate feature absorption similar to what they do in [this paper](./a-is-for-absorption-studying-feature-splitting-and-absorption-in-sparse-autoencoders.md). They train both a vanilla and a Matryoshka SAE with the same number of total features and encoder/decoder architecture (ReLU). The experiment shows that the Matryoshka SAE was able to recover the true hierarchical structure whereas the vanilla SAE was not.

They then do an investigation on a small 4-layer transformer trained on TinyStories. They train SAEs of various sizes and compare the learned features across SAEs. They show an example of feature absorption in vanilla SAEs for a "Female tokens" feature, and claim that similar features were not absorbed in a Matryoshka SAE trained on the same model and data.

Finally, they do a large-scale validation experiment on Gemma 2 2B. They compare against 6 other model architectures using [SAEBench](./SAEBench-a-comprehensive-benchmark-for-sparse-autoencoders-in-language-model-interpretability.md).
- Reconstruction performance: worse than BatchTopK SAEs but better than vanilla
- Downstream performance: cross-entropy comparable with BatchTopK SAEs
- Way less absorption and splitting than BatchTopK for lower sparsities (same metrics as the original [feature absorption paper](./a-is-for-absorption-studying-feature-splitting-and-absorption-in-sparse-autoencoders.md))
- Way better at targeted concept erasure (same metrics as the [spurious correlation removal paper](./evaluating-sparse-autoencoders-on-targeted-concept-erasure-tasks.md))