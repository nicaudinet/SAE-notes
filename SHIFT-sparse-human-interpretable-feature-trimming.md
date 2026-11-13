Classifiers often rely on unintended signals (spurious features). Previous work almost always uses disambiguation data to remove such unintended signals. Instead, they develop Sparse Human-Interpretable Feature Trimming (SHIFT), where they have humans interpret the [sparse-feature-circuits](./sparse-feature-circuits.md) and remove unintended features by hand.

Given labeled training data $D = {(x_i, y_i)}$, a LM-based classifier $C$, and SAEs for various components of $C$, SHIFT works by:
1) Compute the SFC that explains the accuracy of $C$ on inputs from $D$
2) Manually inspect the SFC and evaluate features
3) Ablate from $C$ unintended features
4) Optionally fine-tune $C'$ on data from $D$

## Removing gender signal

They subsample the [Bias in Biographies](https://huggingface.co/datasets/LabHC/bias_in_bios) dataset to create:
- Ambiguous set of only male professors and female nurses
- Balanced set of equal number of male/female professors and male/female nurses

The ambiguous set is the worst-case scenario where the unintended signal (the gender) is perfectly predictive of the profession. Using only this dataset they want to create a classifier which ignores gender and that is therefore accurate on the balanced dataset.

They find that SHIFT almost completely removes the dependence of the classifier on gender. Ablating random SAE features they see no effect, so choosing the correct features to remove is meaningful. Applying SHIFT on neurons directly doesn't work either because they are difficult to interpret. 
