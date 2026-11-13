A transcoder is an approximation of a densely-activating MLP module in a transformer layer with a wider sparsely-activating MLP layer.

They are characterised by:
- A wide one-layer MLP
- ReLU activation function
- L1 regularisation penalty on neuron activations
- Trained to learn MLP outputs from inputs

In equations:
$$
\begin{align}
Z_\text{TC} &= \text{ReLU}(W_e x + b_e) \\
TC &= W_d Z_\text{TC}(x) + b_d \\
\end{align}
$$

where
- $d_{model}$ is the model's embedding dimension
- $d_{features}$ is the number of features in the transcoder (much larger than $d_{model}$)
- $x : d_{model}$ is the input to the MLP layer
- $W_e : d_{features} \times d_{model}$ defines the encoder feature vectors which determine how much each feature should activate
- $W_d : d_{model} \times d_{features}$ defined the decoder feature vectors which determine the direction of the feature in embedding space (and get scaled by the feature activation)
- $b_e : d_{features}$
- $b_d : d_{model}$

Transcoders are trained with the same loss as SAEs which minimises the squared error and adds an $L_1$ sparsity constraint to encourage features to be [[monosemanticity|monosemantic]]:
$$
\mathcal{L}_\text{TC}(x) = \| \text{MLP}(x) - \text{TC}(x) \|_2^2 + \lambda_1 \| z_\text{TC}(x) \|_1
$$