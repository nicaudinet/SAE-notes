---
title: Evaluating Sparse Autoencoders on Targeted Concept Erasure Tasks
tags:
  - paper
---
https://arxiv.org/pdf/2411.18895

---

[SAE](./SAE-sparse-autoencoders.md) developments lacks trusted metrics to evaluate progress. Unsupervised proxy metrics like sparsity and fidelity don't always align with desirable outcomes like interpretability.

To address this they propose measuring SAEs directly on downstream applications. I guess this is a similar argument to what the [End-to-End SAEs](./identifying-functionally-important-features-with-end-to-end-sparse-dictionary-learning.md) are trying to do.

Differences from the original SHIFT:
* They use an LLM judge rather than a human
* They use both [Bias in Biographies](https://huggingface.co/datasets/LabHC/bias_in_bios) and [McAuley Amazon Reviews](https://amazon-reviews-2023.github.io/)
* They remove all unrelated features (spurious and neutral)
* They select top $n$ SAE features according to the absolute attribution score

# Spurious Correlation Removal

==Spurious Correlation Removal== (SRC): a family of evaluations based on [SHIFT](./SHIFT-sparse-human-interpretable-feature-trimming.md) that measures an SAE's ability to disentangle concepts and remove spurious correlations. Requires datasets containing said spurious correlations.

Given a list of natural language concepts $\mathcal{C}$ and a suite of SAEs for a particular model, they follow these steps to determine the best SAE:
1) Train a binary linear classification head for each $c \in \mathcal{C}$ on the model
2) Identify a set of SAE features $\mathcal{F}_c$ for each $c \in \mathcal{C}$.

They do this by looking at the weights of the linear probes trained on the SAE output. The attribution score for a feature with index $i$ on concept $c$ is:
$$
\text{Score}(i,c) = (\textbf{d}_i \cdot \textbf{P})(\bar{\textbf{a}}_\text{pos} - \bar{\textbf{a}}_\text{neg})
$$
where
- $\textbf{d}_i$ is the SAE decoder vector for feature $i$
- $\textbf{P}$ is the weight matrix of the probe for concept $c$
- $\bar{\textbf{a}}_\text{pos}$ is the mean of the feature activations for inputs where $c=1$
- $\bar{\textbf{a}}_\text{neg}$ is the mean of the feature activations for inputs where $c=0$

They also include a component of LLM-judged interpretability to the features.

3) An SAE is high-quality if removing $\mathcal{F}_c$ from the SAE leads to a drop in the classifier for $c$ but not for the classifiers for the other concepts.

The construct the following normalised evaluation score:
$$
S_\text{SHIFT} = \frac{A_\text{ablated} - A_\text{base}}{A_\text{oracle} - A_\text{base}}
$$
where
- $A_\text{base}$ is the accuracy of the probe before ablation
- $A_\text{ablated}$ is the accuracy of the probe after ablation
- $A_\text{oracle}$ is the accuracy of the probe trained directly on the desired concept

# Targeted Probe Perturbation

==Targeted Probe Perturbation== (TPP): generalisation of SCR to all text classification datasets.

Rather than just looking at a target correlation and a spurious correlation, they generalise to multi-class datasets.

For each concept $c \in \mathcal{C}$ they partition the dataset into
1) Samples corresponding to $c$
2) A mix of samples corresponding to the other classes

Let
- $C_i$ be the probe corresponding to a concept $c_j$
- $C_{i,j}$ be the classifier $C_j$ where the features corresponding to $c_i$ have been ablated
- $A_j$ be the accuracy of $C_j$ when classifying $c_j$
- $A_{i,j}$ be the accuracy of $C_{i,j}$ when classifying $c_j$

Then they construct the following target probe perturbation score:
$$
S_\text{TPP} = \underset{i = j}{\text{mean}}(A_{i,j} - A_j) - \underset{i \neq j}{\text{mean}}(A_{i,j} - A_j)
$$
If $i=j$ then we expect the accuracy $A_{i,j}$ to be smaller than $A_j$ since we've removed the features relevant to concept $c_j$. If $i \neq j$ then $A_{i,j} - A_j$ should be small since the features for concept $c_j$ are still present.

# Results

They broadly show that [BatchTopK](./BatchTopK-sparse-autoencoders.md) and [JumpReLU](./jumping-ahead-improving-reconstruction-fidelity-with-JumpReLU-sparse-autoencoders.md) SAEs perform better on their metrics than [standard SAEs](./SAE-sparse-autoencoders.md). The results are not very conclusive though.