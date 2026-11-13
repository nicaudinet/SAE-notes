Simple feed-forward neural networks are invariant under [basis rotations](./basis-rotations-in-neural-networks.md). However, it's been empirically observed that this is not the case in other neural network architectures like [transformer](./transformer-architecture.md) MLP layers or convolutional neural networks. Instead, these networks seem to prefer a particular privileged basis and tend to align some features with neurons.

In [this article](https://transformer-circuits.pub/2023/privileged-basis/index.html) they talk about 

In [toy-models-of-superposition](./toy-models-of-superposition.md) they show a simple neural network which demonstrates this effect,
$$
\begin{align}
h &= \text{ReLU}(Wx) \\
x' &= \text{ReLU}(W^T h + b) \\
\end{align}
$$
where $x$ is the input and $W$ is some non-square weight matrix which maps "features" (rows) to "neurons" (columns). They show that just breaking the symmetry in $h$ by wrapping it with a ReLU aligns the features with the neurons in a structured way.