<iframe width="560" height="315" src="https://www.youtube.com/embed/Q81RR3yKn30?si=CPHMIvpyOkCF_egF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

A regression which adds some bias in order to improve the variance.

The bias is added as a penalty term which depends on the **square of the gradient** and a user-given parameter $\lambda \in \R^+$. The greater the $\lambda$, the more bias is added.

The steeper the gradient, the more small changes in the input affect the output. The purpose of the penalty term is to flatten the gradient (move it towards 0) to make the model less sensitive.

The value for $\lambda$ which results in the lowest variance can be approximated with cross-validation.

In a simple linear regression context
$$
y = m * x + b
$$
we normally train the model to find the gradient $m$ and y-intercept $b$ which minimise the sum of the squared residuals. In ridge regression, you minimise the sum of squared residuals _and_ the a penalty term $\lambda m^2$. 

In general, the penalty term contains all the parameters except for the y-intercept (which doesn't scale from the inputs).

When variables are correlated, ridge regression tends to shrink all the parameters together.