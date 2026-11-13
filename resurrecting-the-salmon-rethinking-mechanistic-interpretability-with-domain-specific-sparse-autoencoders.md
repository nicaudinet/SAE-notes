---
tags:
  - paper
---
https://arxiv.org/pdf/2508.09363?

---

This paper argues that training domain-specific [SAEs](./SAE-sparse-autoencoders.md) mitigates a lot of the [problems](./SAE-failure-modes.md) of generic SAEs, improving both reconstruction accuracy and interpretability. They think this is because broad-domain SAEs tend to represent only common high-frequency patterns due to a fixed latent "budget" and the sparsity constraint. They conclude that domain-specific SAEs work much better in their domain than broad-domain SAEs. The downside is that you need a large corpus and technical know-how to train your own domain-specific SAEs.

The name is a reference to the [fMRI dead salmon](./fMRI-dead-salmon-multiple-comparisons.md).
# Details

The problems of broad-domain SAEs they outline include
- [SAE dark matter](./SAE-dark-matter.md)
- [Feature splitting](./feature-splitting-in-sparse-autoencoders.md)
- [Feature absorption](./feature-absorption-in-sparse-autoencoders.md)
- [Training reproducibility](./sparse-autoencoders-trained-on-the-same-data-learn-different-features.md)

They train [JumpReLU SAEs](./jumping-ahead-improving-reconstruction-fidelity-with-JumpReLU-sparse-autoencoders.md) at layer 20 in Gemma 2 (both 2B and 9B).

They use a dataset constructed from a few different medical QA datasets. For each example they concatenate the question, multiple choice options, correct answer, and any other details into a single string. In total this amounted to ~200K examples and ~50M tokens. They published their dataset [here](./dataset-medical-qa-combined.md).

> Preserving a uniform structure allows us to remove the need to learn a significant number of features that correspond simply to the structure of the text rather than its contents.

## SAE Evaluation

They use 3 unsupervised evaluation metrics.

1. [L0](./vector-norms.md) sparsity: the expected number of active features per input
$$
\E_{\textbf x \sim D} [ \| \textbf f (\textbf x) \|_0 ]
$$

2. Fraction of variance explained where $\V(\textbf x)$ is the sum of variances across all dimensions
$$
1 - \frac{\V(\textbf x - \hat{\textbf x}(\textbf f (\textbf x)))}{\V(\textbf x)}
$$

3. Loss recovered where $\text{CE}(\phi)$ is the average cross-entropy loss of the LLM when a function $\phi : \R^n \to \R^n$ is spliced into the model at the SAE insertion point, $\zeta : \textbf x \mapsto \textbf 0$ is the zero-ablation function, and $\text{Id} : \textbf x \mapsto \textbf x$ is the identity function
$$
1 - \frac{\text{CE}(\hat{\textbf x} ~\circ~ \textbf f) - \text{CE}(\text{Id})}{\text{CE}(\zeta) - \text{CE}(\text{Id})}
$$

They also evaluate interpretability by generating feature explanations and measuring their fidelity. They follow the method from [this paper](./automatically-interpreting-millions-of-features-in-large-language-models.md).

Feature generation is done by sampling examples from each activation decile and passing them onto a language model.

Faithfulness is assessed by treating the interpretation as a classifier which predicts when a feature will activate. A good classifier should exhibit both high precision and recall They evaluate this with LLMs in two ways.

4. Detection: they prompt an LLM with an entire sequence and ask it whether it thinks the feature will activate based on its explanation.

5. Embedding: use the explanation as a query used to retrieve contexts where the feature is active.

Inspired by the [dark matter](./SAE-dark-matter.md) paper they also evaluate the SAE reconstruction error
$$
\text{SaeError}(\textbf x) = \textbf x - \text{SAE}(\textbf x)
$$

They do this in 3 ways:

1. Training a scalar probe that maps $\textbf x$ to $\| \text{SaeError}(\textbf x) \|^2_2$
$$
\textbf a^* =
\argmin{\textbf a \in \R^{(d+1) \times d}}
\|
\textbf a^\top \cdot [\textbf x; 1] - \| \text{SaeError}(\textbf x) \|^2_2
\|^2_2
$$

2. Training a linear probe that predicts the full error, then for each dimension computing the $R^2$ between the true error and the predicted error, then averaging over those $R^2$ values
$$
\textbf b^* =
\argmin{b \in \R^{(d+1) \times d}}
\|
\textbf b \cdot [\textbf x; 1] - \text{SaeError}(\textbf x)
\|^2_2
$$

3. Non-linear fraction of variance unexplained
$$
\begin{align}
\tilde{\textbf x} & = \text{SAE}(\textbf x) + \textbf b^* \cdot \textbf x \\
FUV_\text{nonlinear} & = 1 - R^2(\textbf x, \tilde{\textbf x}) \\
\end{align}
$$




They show that training SAEs on a domain-specific dataset results in:
- 20% more explained variance
- higher loss recovery
- reduced linear residual error
- features more aligned with domain concepts