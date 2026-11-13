Cosine distance or ==cosine similarity== between two vectors $v$ and $w$ is defined as the cosine of the angle between the two vectors:
$$
dist(v,w) = cos(\phi)
$$
This value can also be computed using the geometric definition of the [dot-product](./dot-product.md):
$$
dist(v,w) = \frac{v^T w}{|v||w|}
$$
Properties:
- $dist(v,w) \rightarrow 1$ means that the vectors are close to each other (small $\phi$)
- $dist(v,w) \rightarrow 0$ means that the vectors are far from each other (large $\phi$)