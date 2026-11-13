---
tags:
  - paper
---
https://aclanthology.org/2026.acl-long.1685.pdf

---

Retrieval systems rely on good document embeddings. In multilingual settings however document representations from text encoders contain language identity information alongside the desired semantic information with language information. This leads to a bias towards matching documents in the same language.

They want to fix this post-hoc since many applications rely on pre-computed embeddings which would be expensive to re-compute.

They don't mention [SHIFT](./SHIFT-sparse-human-interpretable-feature-trimming.md) or the [Sparse Feature Circuits](./sparse-feature-circuits.md) paper at all.

They use `multilingual-e5-large` as the text encoder.

They use a modified [TopK SAE](./topk-sparse-autoencoders.md) where they apply the TopK operation _after_ a ReLU.

They identify features by looking at activation frequencies on a language-labelled probe set. 

They identify three different sets of features:
1) Features that activate frequently for a language
2) Features that only activate for a language
3) Features that activate for many languages

They show that their method works well at reducing language identity bias.

# Training

> Train and validation sizes. After filtering, chunking, and balancing, the dataset contains 95,744,230 training segments and 23,936,060 validation segments. Training uses 1 epoch over the training set.

They use the same validation split to estimate the feature activation frequencies. 

Each segment is between 250 and 500 tokens (using e5's tokeniser). 

They also have an auxiliary feature-usage term to discourage dead neurons. If the activation frequency of a neuron falls under a certain threshold, the neuron gets penalised. 