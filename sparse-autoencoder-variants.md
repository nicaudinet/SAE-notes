Variants of [Sparse Autoencoders](./SAE-sparse-autoencoders.md) (SAEs) used to find rich, diverse and monosemantic features from the residual streams of language models.

1) [Top-K SAEs](./topk-sparse-autoencoders.md) use a TopK function to enforce sparsity rather than the [$L_1$ norm](./vector-norms.md)

2) [BatchTopK](./BatchTopK-sparse-autoencoders.md) relax the TopK constraint to the batch level

3) [JumpReLU SAEs](./jumping-ahead-improving-reconstruction-fidelity-with-JumpReLU-sparse-autoencoders.md) use a JumpReLU function rather than standard ReLU

4) [Matryoshka SAEs](./matryoshka-sparse-autoencoders.md) learn nested SAEs simultaneously (used in Gemmascope 2)

5) [OrtSAEs](./OrtSAE-orthogonal-sparse-autoencoders-uncover-atomic-features.md) enforce orthogonality between the learned features by penalising high pairwise cosine similarity between SAE features

6) [Persistent SAEs](./persistent-sparse-autoencoders-learning-feature-timescales-in-language-models.md) learn a persistence coefficient alongside features, separating local evidence from compact persistent state that tracks semantic context

7) [Gated SAEs](./improving-sparse-decomposition-of-language-model-activations-with-gated-sparse-autoencoders.md)

8) [Hierarchical SAEs](./incorporating-hierarchical-semantics-in-sparse-autoencoder-architectures.md)