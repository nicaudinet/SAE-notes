---
title: Feature composition
---
==Feature composition== is a failure mode of [SAEs](./SAE-sparse-autoencoders.md) where features are combined together to minimise the number of active features due to the sparsity constraint.

For example, imagine an SAE has two features:
1) $f_1$ represents the concept of "red"
2) $f_2$ represents the concept of "triangle"

If the SAE encounters a "red triangle" in the training data then it should activate both features.

However, the sparsity term in the loss encourages the SAE to always activate as few features as possible. Instead of keeping both $f_1$ and $f_2$ the SAE might learn to combine the two concepts into a composite $f_3$ which represents the concept of a "red triangle". This could lead to less monosemantic and interpretable features.

This behaviour worsens for larger SAEs as they have a larger "feature budget" and therefore it becomes relatively cheaper to "spend resources" on composite features.

Feature composition also hurts generalisation. Imagine an SAE has features for "red", "blue", "triangle", and "square". Let's also imagine that the data the SAE is trained on only has the contexts "red triangle" and "blue square". Due to feature composition the SAE would then learn features for "red triangle" and "blue square". However, the SAE would now fail to appropriately represent the concepts of "blue triangles" and "red squares".

This failure mode was examined in [this paper](./sparse-autoencoders-do-not-find-canonical-units-of-analysis.md) by Patrick Leask and others using SAE stitching and meta-SAEs.