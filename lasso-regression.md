<iframe width="560" height="315" src="https://www.youtube.com/embed/NGf0voTMlcs?si=rvShHouMOcyXWmml" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
Very similar to [ridge-regression](./ridge-regression.md) but uses the absolute value of the gradient in the penalty term rather than the square.

Lasso regression can shrink the gradient all the way to 0, whereas ridge regression can only shrink it asymptotically to 0. Therefore, it is a bit better at reducing variance in models with lots of useless variables. Helps for interpretability as well.

Ridge regression tends to do a little better than lasso regression in models where most variables are useful.

When variables are correlated, lasso regression tends to choose one of them and eliminates the others.