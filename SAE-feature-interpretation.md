[SAEs](./SAE-sparse-autoencoders.md) learn interpretable features ([sometimes](./SAE-failure-modes.md)). But how do we generate those interpretations?

The standard way is to use an autointerpretability pipeline. This idea was first introduced in [this paper](./automatically-interpreting-millions-of-features-in-large-language-models.md) and [this blog post](./open-source-automated-interpretability-for-sparse-autoencoder-features.md) by EleutherAI researchers. The [HypotheSAE](./HypotheSAE-sparse-autoencoders-for-hypothesis-generation.md) paper also has a nice discussion of their autointerp pipeline. Autointerp is more of an art than a science at this point though.

The central idea of these pipelines is to use an LLM to generate interpretations based off of training samples for which the feature activates the most:
```
1) Train your SAE

2) Record feature activations for the final SAE on the training data

3) For each feature:
    a) Find the top activating samples
    b) Prompt an LLM for an interpretation given the top samples
```

You can also evaluate the fidelity of an interpretation:
```
1) For each sample in a held-out dataset:
    a) Prompt an LLM to predict activation given sample text and interpretation 
    b) Run the sample through the SAE and record the feature activation

2) Compute the accuracy or F1 score
```
One can then generate multiple explanations for each feature and pick the most faithful one.