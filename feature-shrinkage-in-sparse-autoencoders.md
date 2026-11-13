==Feature shrinkage== is the systematic under-estimation of activation magnitudes in L1-regularised [SAEs](./SAE-sparse-autoencoders.md).

L1 regularisation encourages all activations to be as small as possible, even activations for features that _should be active_. This leads to worse reconstruction fidelity for a given sparsity level.

[JumpReLU](./jumping-ahead-improving-reconstruction-fidelity-with-JumpReLU-sparse-autoencoders.md) mitigates this because it thresholds whether a feature is active or not by a learnable parameter $\theta$. If a feature activation is above $\theta$ it goes through unpenalised, but if it doesn't then it's set to 0.

Rather than using L1 regularisation, [BatchTopK](./BatchTopK-sparse-autoencoders.md) SAEs use an L0-style approach instead. This also ensures that the activation selection and magnitude are decoupled. Sparsity is controlled architecturally.

This is a similar story to Lasso vs. Ridge regression.