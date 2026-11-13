In a [linear model](./linear-regression.md), the variance explained is the fraction of $\text{Var}(Y)$ attributable to some input variable $X$.

Let $Y = \beta X + \epsilon$ and $X \perp \epsilon$. Then:
$$
\V(Y) = \beta^2 \V(X) + \V(\epsilon)
$$

The variance explained by X is then the ratio:
$$
R^2 = \frac{\beta^2 \V[X]}{\V[Y]}
$$