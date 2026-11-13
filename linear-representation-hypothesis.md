The Linear Representation Hypothesis (LRH) is the hypothesis that, in [[neural-networks|neural networks]] and in particular [LLMs](./large-language-model.md), features of the input are represented as [linear](./linearity.md) directions in the latent activation space.

[LRH motivation.](./motivation-for-the-linear-representation-hypothesis.md)

Concretely, this means that for a concept $c$ then
$$
f_c(\textbf{h}) \approx \textbf W_c^\top \textbf h + b_c
$$
where
- $\textbf h \in \R^d$ is the model's hidden activation vector
- $\textbf W_c^\top \in \R^d$ is the direction for concept $c$
- $f_c(\textbf h)$ measures the presence and strength of concept $c$

A basis-aligned model is one where all $W_c$ are one-hot vectors, and is partially aligned when the $W_c$ are sparse.

If the LRH is true, then neural representations can be decomposed into independent understandable features. Given that neural networks and most relationships captured by data are non-linear, features are most likely non-linear functions of the inputs. However, here are  some arguments for why linear representations might be true:
- Accessibility: if a feature in a previous layer is represented linearly, a neuron in the next layer can "select it" consistently
- Allow for non-local generalisations which increase statistical efficiency