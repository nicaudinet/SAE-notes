---
tags:
  - notes/paper
---
https://arxiv.org/pdf/2502.04878

---

They argue that a key challenge of mechanistic interpretability is to identify correct units of analysis which can be used to collectively explain a neural network's function. They should be unique, complete and atomic.

To compare features of different sizes they use ==SAE stitching== where they swap clusters of features between SAEs based on [cosine similarity](./cosine-similarity.md). They use this to show that larger SAEs can learn novel features, which indicates that the smaller SAEs can miss out on information altogether (are incomplete).

However, they also show that some features from the larger SAE are based on multiple features from the smaller SAE, indicating the presence of [feature composition](./feature-composition-in-sparse-autoencoders.md). To investigate this they use ==meta-SAEs== where they train an SAE on the decoder matrix of another SAE. With this, they show that features from the original SAE often decompose into interpretable concepts (e.g. "Einstein" decomposes into "scientist", "Germany", and so on).