---
tags:
  - ideas/project
---
[This paper](./sparse-feature-circuits.md) paper introduces the idea of Sparse Feature Circuits (SFCs), subgraphs of the causal graph implied by a neural network with interpretable features. They build on [Sparse AutoEncoders (SAEs)](./SAE-sparse-autoencoders.md) to find interpretable features, and linear approximations of the [indirect effect](./natural-direct-and-indirect-effects.md) to find causal links between the features. They further show that humans can use these causal graphs to efficiently remove unintended signals from the graph (SHIFT) and that they can discover these graphs at scale in an unsupervised manner.

This could be really useful! For example, imagine that I want a to make a tool for moderating Reddit posts in an interpretable way. A basic approach could be to take a dataset of posts where we also have an expert-coded removal label. Then, we could train a classifier (e.g. fine-tuned BERT) on the dataset to give probabilities that the post should be removed, and remove all posts above a certain threshold. This might work well in benchmarks, but it's hard to explain _why_ a post was removed. Instead, we can train an SFC using the labeled data, improve the circuit with SHIFT, and use the circuit as an interpretable classifier.

One of the questions I had when reading this work was: can we somehow extract these features into independent networks? Potential advantages of doing this could be:
- Efficiency: if I know I only want to perform a single task anyway, I don't need to run the full language model
- Interpretability: if the extracted networks are small enough they might be easier to interpret / understand. We could even adapt the structure of the networks to "fit" the 
- We can use SHIFT to remove unintended features by hand from the circuits as we extract them to make them more robust

If this works, I can imagine making a "language toolbox" with composable "language tools" which could be used for program synthesis for language tasks! This would be interesting for:
- Validation: if we can use the extracted circuits productively, this validates that the circuits actually do what they're supposed to do
- Interpretability: again, if the extracted circuits are small enough and can compose together, we might be able to construct language processing tools which we can inspect and understand more easily