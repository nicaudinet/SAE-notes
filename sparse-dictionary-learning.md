Sparse dictionary learning (or sparse coding) represents each data point $x \in \mathbb{R}^n$ as a sparse linear combination of the columns ("atoms") of a learned dictionary $D \in \mathbb{R}^{n \times m}$:
$$
x \approx D z \quad \text{with } z \in \mathbb{R}^m \text{ mostly zero}
$$

The dictionary is usually overcomplete ($m > n$), so there are more atoms than dimensions. This only works because of the sparsity: with $m > n$ there are infinitely many dense $z$ that reconstruct $x$, but few sparse ones. Dictionary and codes are learned jointly by minimising reconstruction error plus a sparsity penalty:
$$
\min_{D, z} \; \|x - D z\|_2^2 + \lambda \|z\|_1
$$
where the columns of $D$ are constrained to unit norm, otherwise the penalty could be dodged by shrinking $z$ and growing $D$.

Classic sparse coding (Olshausen & Field, 1996) solves a separate optimisation problem for $z$ for every input. [SAEs](./SAE-sparse-autoencoders.md) amortise this: an encoder predicts the code $z$ in a single forward pass, and the decoder weights play the role of the dictionary $D$.

In interpretability, this is the natural tool if the [superposition hypothesis](./superposition-hypothesis.md) and the [sparsity hypothesis](./sparsity-hypothesis.md) hold: activations are a sparse combination of more feature directions than there are neurons, which is exactly the model sparse dictionary learning assumes.
