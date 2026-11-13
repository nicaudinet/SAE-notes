A variant of the [transcoder](./transcoder.md) where features trained at layer $\ell$ directly affect features trained for _all_ downstream layers $\ell + 1$ to $L$, not just features at layer $\ell+1$.

Cross-layer transcoders are thought of as spanning the whole model rather than just an MLP module in a particular layer. All features at all layers are trained all once.

The key advantage of doing it this way is to simplify the circuits trained on the features since the signal between features in non-neighbouring layers don't have to go through each intermediate layer anymore.

Originally proposed/popularised in the [Circuit Tracing](./circuit-tracing-revealing-computational-graphs-in-language-models.md) blog post by Anthropic.

# Running

Let:
- $x^\ell$ be the input to the MLP module at layer $\ell$
- $y^\ell$ be the output of the MLP module at layer $\ell$

Activations of the cross-layer transcoder at layer $\ell$ are computed with:
$$
a^\ell = \text{JumpReLU}(W_{enc}^\ell x^\ell)
$$
where $W_{enc}^\ell$ is the encoder matrix for features at layer $\ell$.

The cross-layer transcoders prediction of the MLP output  at layer $\ell$ are computed taking into account activations from all previous layers:
$$
\hat{y}^\ell = \sum_{\lambda = 1}^\ell W_{dec}^{\lambda \to \ell} a^\lambda
$$
where $W_{dec}^{\lambda \to \ell}$ is the decoder matrix for features from layer $\lambda$ to layer . Features at layer  have a separate decoder matrix for each subsequent layer $\ell + 1$ to $L$.

# Training

Cross-layer transcoders are trained by minimising $\text{MSE}(y^\ell, \hat{y}^\ell)$ alongside a sparsity condition:
$$
\begin{align}
L_\text{MSE} &= \sum_{\ell = 1}^L \| \hat{y}^\ell - y^\ell \|^2 \\
L_\text{sparsity} &= \lambda \sum_{\ell = 1}^L \sum_{n=1}^N \tanh(c \cdot \|W_{dec,n}^\ell \| \cdot a_n^\ell)
\end{align}
$$
where $W_{dec,n}^\ell$ is the concatenation of all decoder vectors for feature $n$ and $\lambda$ and $c$ are hyper-parameters.