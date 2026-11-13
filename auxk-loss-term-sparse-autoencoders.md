A term added to the SAE training loss in order to combat the [dead neurons](./dead-neurons-in-sparse-autoencoders.md) in [TopK SAEs](./topk-sparse-autoencoders.md). Originally from [this post from Anthropic](https://transformer-circuits.pub/2024/jan-update/index.html#dict-learning-resampling), but this particular formulation is from the [HypotheSAE](./HypotheSAE-sparse-autoencoders-for-hypothesis-generation.md) paper.

In the paper, they use the following loss function
$$
\begin{align}
\mathcal L_\text{TopK} & = \| e_i - \hat e_i \|_2^2 \\
\mathcal L_\text{AuxK} & = \| W_\text{dec} z_i^\text{AuxK} - (e_i - \hat e_i) \|_2^2 \\
\mathcal L & = \mathcal L_\text{TopK} + w_\text{aux} \mathcal L_\text{AuxK}
\end{align}
$$
Once a neuron has not been activate in the last 256 steps it is considered "dead" and enters into the dead neuron pool. The $\mathcal L_\text{AuxK}$ term gives an alternative gradient path that reaches into the dead neuron pool to try to get them unstuck. It takes the top $k_\text{aux}$ dead neurons and asks them to reconstruct the reconstruction error $e_i - \hat e_i$ (what they normal neurons missed). They reconstruct $e_i - \hat e_i$ rather than the input because this encourages the dead neurons to specialise into representing what the normal neurons are missing. They set $k_\text{aux} = 2k$ throughout.