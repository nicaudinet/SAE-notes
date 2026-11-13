---
title: Identifying Functionally Important Features with End-to-End Sparse Dictionary Learning
tags:
  - paper
---
https://proceedings.neurips.cc/paper_files/paper/2024/file/c212c1b88395ab68d5e1671c17883ec6-Paper-Conference.pdf

---

They argue that the features learned by traditional [SAEs](./SAE-sparse-autoencoders.md) are only indirectly aligned with the computational structure of the network.

This is a problem because, due to the sparsity and reconstruction loss, an SAE is incentivised to waste capacity [splitting](./feature-splitting-in-sparse-autoencoders.md) features based on the structure of the dataset rather than learning features which explain the network's performance. Indeed, there is nothing in the architecture or loss function of traditional SAE which forces the features to be "functionally important".

Instead, they propose changing the loss function to:
1) Promote SAE feature sparsity (same as before)
2) Minimise the KL divergence between the output distribution of the original model and the output distribution of a model with the SAE replacing the sub-component it's trying to explain

Optionally, one can also add terms for the reconstruction loss of all internal activations downstream of the SAE to minimise the likelihood that the SAE learns to take different computational paths than the original model.

They find that:
- End-to-end SAEs are a Pareto improvement over local SAEs. They need about half the features activated to explain the same amount of performance than traditional SAEs.
- End-to-end SAEs have worse reconstruction loss at each layer despite similar output distributions
- End-to-end SAEs have more orthogonal features than traditional SAE
- End-to-end SAE features are not robust across random seeds, but traditional SAE features and end-to-end SAE features trained with the additional downstream reconstruction loss term are
- End-to-end SAE features do not always align with traditional SAE features
- No marked difference in feature interpretability

However, e2e SAEs take longer to train.