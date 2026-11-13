==Feature absorption== is a failure mode of [SAEs](./SAE-sparse-autoencoders.md) where parent features fail to activate in a seemingly random fashion due to the sparsity constraint when a hierarchy exists between features.

For example, take these two features:
1) $f_1 = \texttt{starts with "s"}$
2) $f_2 = \texttt{starts with "stop"}$.

$f_1$ is the parent of $f_2$ because $f_1$ always activates whenever $f_2$ activates. If the `stoppage` token is in the input we would then expect both $f_1$ and $f_2$ to activate at its position.

However, the sparsity term in the loss constantly pushes the SAE to activate as few features as possible. The SAE will tend to activate only $f_2$ as this still achieves perfect reconstruction but also increases sparsity. This leads to parent features not activating in a seemingly random fashion.

This failure mode was first coined and studied in the [A is for Absorption](./a-is-for-absorption-studying-feature-splitting-and-absorption-in-sparse-autoencoders.md) paper by Chanin et al.