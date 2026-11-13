---
tags:
  - paper
---
https://arxiv.org/pdf/2501.16615

---

They show that SAEs trained on the same model and data, differing only by their random seed, learn different sets of features.

ReLU SAEs trained with an L1 sparsity loss seem less seed-dependent than [TopK SAEs](./topk-sparse-autoencoders.md).

They test this over multiple layers in 3 LLMs, two datasets, and multiple SAE architectures.

They conclude that SAEs offer a pragmatically-useful decomposition rather than an exhaustive and universal list of "truly used" features.