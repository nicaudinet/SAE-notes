A good SAE must overcome several challenges during it's training. Here are a few.

1) [Dark matter:](./SAE-dark-matter.md) when the SAE features is an incomplete description of the model's representations, usually indicated by a large portion of the SAE error being linearly predictable from input activations.

2) [Dead Neurons:](./dead-neurons-in-sparse-autoencoders.md) when features are never given training signal during training and are therefore never used. Particularly problematic in [TopK SAEs](./topk-sparse-autoencoders.md).

3) [Training reproducibility:](./sparse-autoencoders-trained-on-the-same-data-learn-different-features.md) when SAEs are retrained with different random initialisations they often identify different sets of features.

4) [Feature collapse:](./feature-collapse-in-sparse-autoencoders.md) when features tend to duplicate each other or die due to tensions between the reconstruction and sparsity terms in the loss function.

5) [Feature splitting:](./feature-splitting-in-sparse-autoencoders.md) when useful high-level features tend to be partitioned into multiple more fine-grained and context-dependent variants.

6) [Feature composition:](./feature-composition-in-sparse-autoencoders.md) when SAEs learn features which are compositions of more atomic features.

7) [Feature absorption:](./feature-absorption-in-sparse-autoencoders.md) when a hierarchy exists between features, parent features can fail to activate in a seemingly random fashion due to the sparsity constraint.

8) [Feature shrinkage:](./feature-shrinkage-in-sparse-autoencoders.md) when feature activation magnitudes in SAEs with [L1](./vector-norms.md)-regularisation are pushed towards 0 even when they are supposed to be active, hurting reconstruction.