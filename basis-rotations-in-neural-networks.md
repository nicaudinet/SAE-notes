Let $f(x)$ be a simple [[feed-forward-neural-network]]:
$$
f(x) = \phi(W^{(2)} \phi(W^{(1)} x + b^{(1)}) + b^{(2)})
$$

Then the network is representationally invariant under [basis rotations](./basis-rotation.md). This is because, given some input space rotation $x' = Rx$, we can define a transformed network where we rotate the weights back to the original transform with $W^{(1)} \to W^{(1)} R^t$:
$$
f'(x) = \phi(W^{(2)} \phi(W^{(1)} R^T x + b^{(1)}) + b^{(2)})
$$
and then $f(x) = f'(x')$. Therefore, the representation power of the network stays the same under basis rotation.

Additionally, this means that when we train a neural network, the features learned by a neural network might make more sense in some other rotation of the input space for any given layer. Because of this, in mechanistic interpretability researchers tend to train [SAE-sparse-autoencoders](./SAE-sparse-autoencoders.md) to identify human-understandable features in the "right" rotation space.