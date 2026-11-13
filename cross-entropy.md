Cross-entropy measures how different two probability distributions are.

It is defined as:
$$
H(p,q) = \underset{x \sim p}{\E} [-\log q(x)] = -\sum_x p(x) \log q(x)
$$
In other words, it is the average number of bits you'd need to encode samples from $p$ if you use a code optimised for $q$ instead of $p$.

Whereas [Shannon entropy](./shannon-entropy.md) only measures the intrinsic randomness of a distribution, cross-entropy also includes the differences between the two distributions. They are related by the [[kullback-leibler-divergence|KL divergence]]:
$$
H(p,q) = H(p) + D_{KL}(p\|q)
$$

For example, let:
1) $p(\cdot)$ be the real next-word distribution as observed in the dataset 
2) $q(\cdot)$ be the next-word distribution learned by a language model

Then, for a single example $x^*$ where $p(x^*) = 1$ the cross-entropy boils down to the negative log probability of the model getting the right answer:
$$
H(p,q) = -\log q(x^*)
$$

Over a whole dataset  of $N$ words we get the average negative log-likelihood.
