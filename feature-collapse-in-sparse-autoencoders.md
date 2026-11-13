---
title: Feature collapse
---
==Feature collapse== is a failure mode of [SAE](./SAE-sparse-autoencoders.md)  training where features tend to duplicate each other or "die" (never activate).

The loss does not explicitly encourage feature diversity. Multiple features can therefore converge to similar directions and optimisation can get stuck in the local minimum. This can also result in [dead neurons](./dead-neurons-in-sparse-autoencoders.md) if one of the features ends up dominating due to sparsity.

Already in [Towards Monosemanticity](./towards-monosemanticity.md) they noticed this behaviour and found that they got better results if during training they periodically check for neurons which are not activating and reinitialise them.

As of early 2026 the leading approaches to counteract feature collapse are [JumpReLU SAEs](./jumping-ahead-improving-reconstruction-fidelity-with-JumpReLU-sparse-autoencoders.md) and [BatchTopK](./BatchTopK-sparse-autoencoders.md). [OrtSAE](./OrtSAE-orthogonal-sparse-autoencoders-uncover-atomic-features.md) explicitly adds feature diversity to it's loss.

Another thing that seems to help is constraining decoder columns to [unit norm](./vector-norms.md), particularly for deeper SAEs.