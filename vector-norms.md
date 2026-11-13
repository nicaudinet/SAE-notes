Norms allow one to measure the magnitude of vectors.

The ==$L_0$ norm==, a.k.a. the "sparse norm", counts the number of non-zero elements in the vector.

The ==$L_1$ norm==, a.k.a. the "Manhattan norm", sums the absolute values of all the elements in the vector:
$$
\| x \|_1 = \sum_{i=1}^n |x_i|
$$

The ==$L_2$ norm==, a.k.a. the "Euclidean norm", sums the square of the values of all the elements in the vector and takes the square root:
$$
\| x \|_2 = \sqrt{\sum_{i=1}^n x_i^2}
$$

The ==$p$-norm== is a generalisation of the $L_1$ and $L_2$ norms. For $p \geq 1$, the $p$-norm is defined as:
$$
\| x \|_p := \left( \sum_{i=1}^n |x_i|^p \right) ^\frac{1}{p}
$$

The $L_\infty$ norm, a.k.a. the "infinity norm" or the "max norm", takes the maximum of the absolute values of all the elements in the vector:
$$
\| x \|_\infty = \text{Max}_{i=1}^n |x_i|
$$