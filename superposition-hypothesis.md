Notes on the superposition hypothesis from [Toy Models of Superposition](./toy-models-of-superposition.md).

![](./Pasted%20image%2020261113095717.png)

Image from [the-state-of-mechanistic-interpretability-for-AI-safety](./the-state-of-mechanistic-interpretability-for-AI-safety.md).

# The Superposition Hypothesis

==Superposition== is when models represent more features than they have dimensions in their representation. Compression beyond linear models at the cost of "interference".

Linear models cannot represent more features than dimensions. The best they can do is represent the principal components. Non-linearity enables superposition.

==Polysemantic neurons== are neurons that respond to several unrelated concepts.

==Monosemantic neurons== are neurons that relate to a single feature. 

According to the Johnson-Lindenstrauss lemma, it is possible to have $\exp(n)$ pair-wise almost-orthogonal vectors with cosine similarity under some $\epsilon$ in an $n$-dimensional space.

Compressed sensing - in general you lose information when you project a vector into a lower dimensional space (surjection), but when you can recover a lot more of the original vector if you know that it was sparse.

Features are represented as almost-orthogonal vectors, so activating a feature slightly activates other features as well. This noise/interference might be tolerated in exchange for the ability to represent way more features.

Neural networks might be simulating much larger basis-aligned models ("disentangled models").

[Demonstrating superposition](./demonstrating-superposition.md) experiment.
