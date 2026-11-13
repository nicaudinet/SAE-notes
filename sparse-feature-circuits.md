---
tags:
  - notes/paper
---
**Sparse Feature Circuits: Discovering and Editing Interpretable Causal Graphs in Language Models** 
Paper by Samuel Marks et al.
https://arxiv.org/pdf/2403.19647

---

[sparse-feature-circuits-running-code-notes](./sparse-feature-circuits-running-code-notes.md)

---

This paper introduces the idea of Sparse Feature Circuits (SFCs), subgraphs of the causal graph implied by a neural network with interpretable features. They build on [SAE-sparse-autoencoders](./SAE-sparse-autoencoders.md) to find interpretable features, and linear approximations of the [indirect effect](./natural-direct-and-indirect-effects.md) to find causal links between the features. They further show that humans can use these causal graphs to efficiently remove unintended signals from the graph (SHIFT) and that they can discover these graphs at scale in an unsupervised manner.

Key challenge of interpretability: explained unanticipated model behaviours at scale
- Use fine-grained components with narrow, interpretable roles
- Search efficiently over combinatorial space of causal circuits

==Sparse Feature Circuits== - causally implicated subnetworks in language models with interpretable features
- [Sparse AutoEncoders (SAE)](./SAE-sparse-autoencoders.md) for features
- Linear approximations to identify SAE features efficiently

# Attributing causal effects

Causality is attributed via the [indirect effect](./natural-direct-and-indirect-effects.md). If $m$ is a metric over a causal graph and $a$ is a node in the causal graph, then the importance of $a$ on a pair of inputs $(x_{clean}, x_{patch})$ is
$$
IE(m; a; x_{clean}, x_{patch}) = m(x_{clean} \mid do(a = a_{patch})) - m(x_{clean})
$$
where $a_{patch}$ is the value that $a$ takes when computing $m(x_{patch})$.

For example, let:
- $x_{clean}$ = "The teacher"
- $x_{patch}$ = "The teachers"
- $m = \log P(\text{``are"} \mid x) - \log P(\text{``is"} \mid x)$

Then, if we get a large IE value for $a$ that means that that neuron plays an important part in getting the model to output "are" vs. "is".

Computing the indirect effect in this way for many $a \in \R^d$ is computationally expensive. Instead, they use linear approximations that can compute many $a$s in parallel.
- Simple approximation: attribution patching
- Improved approximation based on integrated gradients
- Use zero ablation when we only have one input ($a_{patch} = 0$)

# Method
- Language Model $M$
- SAEs for various submodules of $M$
- Dataset $D$ of contrasting pairs ($x_{clean}, x_{patch})$ or single inputs $x$
- Metric $m$ dependent on $M$'s output 

Can substitute the SAEs and their errors for the components they model in the network. With this view, $M$ becomes a computation graph $G$ of SAE feature activations or errors.

Then, they compute the IE for each node in $G$ and each sample in $D$ using linear approximations and filter out nodes whose average IE is below some threshold $T_N$. They do the same for edges.

## Discovering SFCs for subject-verb agreement tasks

The tasks involve matching the subject number ("athlete" vs. "athletes") with the correct verb conjugation ("do" vs. "does").

They compare the SFCs with circuits trained with equivalent methods on the neurons themselves. They evaluate the circuits for interpretability, faithfulness and completeness.

**Interpretability** - they ask crowd workers to rate the interpretability of SFCs, neural features, and some baselines. They find that SFC features are significantly more interpretable

**Faithfulness** - Given circuit $C$ and metric $m$, let $m(C)$ be the average value of $m$ over some dataset $D$ where all nodes outside of $C$ are mean-ablated. Let $M$ be the full model, and $\emptyset$ the empty circuit. Faithfulness then captures the proportion of the model performance explained by the circuit $C$, and is then measured as:
$$
F(C) = \frac{m(C) - m(\emptyset)}{m(M) - m(\emptyset)}
$$

**Completeness** - are there parts of the model that the features cannot explain? Measured as the faithfulness of the complement of the circuit, $F(M \setminus C)$ 
# Removing unintended signals

They describe the [SHIFT](./SHIFT-sparse-human-interpretable-feature-trimming.md) method for removing unintended signals from a text classifier built on activations from a large language model.
# Unsupervised Circuit Discovery at Scale

Almost automated interpretability pipeline:
- Input: text corpus (large subset of The Pile)
- Output: thousands of SFCs for discovered model behaviours

1) Discover model behaviours via clustering
2) For each behaviour, compute the circuit

---

- Ok but like reductionism is a thing ... what if those narrow fine-grained components don't actually exist? What about the [FER](./the-fractured-entangled-representation-hypothesis-FER.md) hypothesis?
- Why do they filter out nodes and edges with low average
- How does this relate to the [[causal-abstraction]] work?

[extracting-sparse-feature-circuits](./extracting-sparse-feature-circuits.md)