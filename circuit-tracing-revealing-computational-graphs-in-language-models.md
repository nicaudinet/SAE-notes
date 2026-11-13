---
tags:
  - notes/paper
---
https://transformer-circuits.pub/2025/attribution-graphs/methods.html

---

Their general approach to understanding the mechanics of language models:
1) Find good, interpretable features
2) Describe how the features interact in circuits

Summary: To identify features they  use a variant of [transcoders](./transcoder.md) rather than [sparse autoencoders](./SAE-sparse-autoencoders.md). They use cross-layer transcoders where features read from one layer and write to all following ones. They compute attribution graphs for individual prompts, which they prune for interpretability. The graphs have linear attribution between features, achieved by freezing the attention non-linearities and substituting the MLP non-linearities with the transcoders.

# Building an Interpretable Replacement Model

They use the [cross-layer-transcoder](./cross-layer-transcoder.md) as the mechanism to find interpretable features in the MLP modules.
