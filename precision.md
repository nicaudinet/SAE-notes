For a [binary-classifier](./binary-classifier.md), ==precision== is the fraction of samples classified as positive that were classified correctly:
$$
\text{Precision} = \frac{TP}{TP+FP} = \frac{\text{true positives}}{\text{all samples classified as positive}}
$$
In other words, if by "positive" we mean "relevant":
$$
Precision = \frac{\text{relevant retrieved instances}}{\text{all retrieved instances}}
$$