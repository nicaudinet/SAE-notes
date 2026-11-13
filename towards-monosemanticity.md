---
tags:
  - paper
---
https://transformer-circuits.pub/2023/monosemantic-features/index.html

---

Mechanistic interpretability is about [[reductionism|reducing]] neural networks into easier-to-understand smaller components, which can then be used to understand the whole. They argue this is the only way to understand what is going on as otherwise the space becomes too big ([[curse-of-dimensionality]]).

Neurons are often not a good component to study since they can be [[polysemanticity|polysemantic]]. Instead they use features form [SAE-sparse-autoencoders](./SAE-sparse-autoencoders.md) as in their previous work [toy-models-of-superposition](./toy-models-of-superposition.md). 

Autoencoder size gives different "resolutions" for understanding the same object (features appear to group into families)

# Problem Setup
They look at "the simplest language model we profoundly don't understand". In particular, they analyse a transformer model with a single layer and 512 hidden units in the MLP layer. They train SAEs only on the MLP layer.

They decompose activation vectors into features using linear matrix factorisation:
$$
x^j \approx \sum_i f_i(x^j) d_i + b
$$
where
- $x^j$ is the activation vector of length $d_{MLP}$ for datapoint $j$
- $f_i(\cdot)$ is the feature $i$ and $f_i(x^j)$ is the activation of feature $i$ for datapoint $j$
- $d_i$ is a unit vector in activation space, the "direction" of feature $i$
- $b$ is a bias

Features are represented by [SAE-sparse-autoencoders](./SAE-sparse-autoencoders.md) with symmetric encoding and decoding:
$$
f_i(x) = \text{ReLU}(W_e(x - b_d) + b_e)_i
$$

This is a form of [[sparse-dictionary-learning]].

SAE features are useful if:
- We can understand under what conditions it activates
- We can understand what it's downstream effects are
- It explains a significant portion of the MLP layer (measured via loss)

They discard architectural approaches (forcing neurons to be monosemantic) because
- There is a large performance hit in these models
- Inducing activation sparsity didn't work
- Neurons can be polysemantic even without superposition as representing multiple features ambiguously can sometimes result in a lower loss than representing a single feature and ignoring the rest
- They had a bit more success in inducing monosemanticity using MSE losses rather than cross-entropy, but it was not enough to convince them to pursue this approach

# Detailed Investigations of Individual Features

Demonstration of some monosemantic features which respond to:
- Text written in Arabic
- DNA sequences
- base64 strings
- Text written in Hebrew script

Specificity: when the feature is active, the context is usually present

Sensitivity: when the context is present, the feature is usually active

# Global Analysis
"How interpretable are the rest of the features?"

How interpretable is the typical feature?
- Human judgement - score neuron and feature interpretability with a scoring rubric (blind). Overall features seemed much more interpretable, with the annotator not being able to even form a hypothesis for what the neuron was doing for more than half of the examples
- Automated interpretability with activations - generate explanations of features with Claude based on examples of tokens where the feature activates, then use the explanations to predict whether the feature activates on previously unseen tokens. Claude did better for features than neurons.
- Automated interpretability with logit weights

How much of the model does our interpretation explain?
- 79% of log-likelihood loss provided by the MLP layer is recovered from the features
- They consider "to what extent does a feature-based interpretation explain model behaviour?" to be an important open question

Do features tell us about the model or the data?
- The interesting properties of the learned features could be due to spurious correlations in the dataset (rather than something the model learned)
- They train features on a version of the model with random weights, and could not find good interpretations for features (except for the single-token ones)

# Phenomenology
What lessons can the features teach us about neural networks?

Inspired from phenomenology in physics. Focused on more abstract properties and patterns. 

Feature motifs
- context features (e.g. DNA)
- token-in-context features (e.g. `<` in HTML) - there are _a lot_ of these apparently (especially after feature splitting when using large SAEs)
- trigram features - some memorisation-like behaviour
- "action features" vs "input features" in one-layer models
    - action features increase the probability of generation
    - input features recognise the pattern in the inputs

Feature splitting
- Features tend to appear in clusters (especially with large numbers of total features)
- The clusters are tight: similar features have small angles between them
- Features don't always split in a neat tree-like pattern, but can merge with features from other clusters etc.
- Features which seem like bugs:
    - Single-token features which fire of every instance of a particular token. Strange that the model implements this in the MLP layer. Explanation with feature splitting is that actually the model has learned a bunch of features that activate on that token in different contexts
    - Multiple features for a single context

Universality
- Do the same features appear across different models?
- They find that there's good evidence for universality both between models they trained and compared to the rest of the literature

"Finite State Automata"
- What about assemblies of feature?
- One-node system example: activation of the base64 feature makes it more likely to generate strings that trigger it again when generating the next token
- Two-node system example: all caps snake case
- In more complex cases with larger feature sets they observe memorisation of certain phrases like "A PARTICULAR PURPOSE"

# Discussion
[toy-models-of-superposition](./toy-models-of-superposition.md) discussed isotropic superposition, where features in superposition pushed away from each other to limit inference. When studying more complex models in this work, however, they found that certain features cluster together - possibly because they produce similar actions (e.g. features that match different kinds of base64 strings all want to produce base64-like strings).

Features are also not necessarily one-dimensional: feature manifolds.