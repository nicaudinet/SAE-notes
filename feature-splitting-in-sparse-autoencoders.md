---
title: Feature splitting
---
==Feature splitting== is a phenomenon observed when scaling up [SAEs](./SAE-sparse-autoencoders.md) where features tend to be partitioned into multiple more specific features which represent smaller portions of the dataset. 

For example, whereas in a small SAE we might get a feature for "dog", in a large SAE we might only get features like "dog in a park context", "metaphorical use of the word dog", "dog anatomy", and so on.

We usually _want_ the SAEs to capture fine-grained monosemantic features. However, this also means that we will miss out on more high-level features. 

In the limit of large SAEs each individual datapoint would be represented with its own feature.

Approaches to mitigate feature splitting include:
- [Matryoshka SAEs](./learning-multi-level-features-with-matryoshka-sparse-autoencoders.md)
- [End-to-end SAEs](./identifying-functionally-important-features-with-end-to-end-sparse-dictionary-learning.md)

This behaviour was already documented in [Towards Monosemanticity](./towards-monosemanticity.md) and was further expanded on in [Scaling Monosemanticity](./scaling-monosemanticity.md). The [absorption](./a-is-for-absorption-studying-feature-splitting-and-absorption-in-sparse-autoencoders.md) paper by Chanin et al. also discusses feature splitting.
