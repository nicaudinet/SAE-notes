The logistic regression models the [log-odds](./log-odds.md) of belonging to a class as a linear relationship. This is expressed as:
$$
\log \left( \frac{P(Y=1 \mid X)}{1 - P(Y=1 \mid X)} \right) = \beta_0 + \beta_1 X_1 + \ldots + \beta_n X_n
$$
where $X$ is a vector of continuous or categorical variables and $Y$ is a binary class variable. For example, given the weight of a mouse, predict the probability that the mouse is obese or not.

In other words, the logistic regression models the probability distribution of belonging to a class as a [logit-function](./logit-function.md) $\sigma(\cdot)$ of a linear combination of the coefficients:
$$
P(Y=1 \mid X) = \sigma(\beta_0 + \beta_1 X_1 + \ldots + \beta_n X_n)
$$

Logistic regression is often used for classification: if the probability of the event happening is above 50% then assign to class 1, else assign to class 0.

Differences with [linear-regression](./linear-regression.md):
- It predicts a binary outcome rather than a continuous one
- It fits a [logistic curve](./logit-function.md) rather than a line
- Trained via [maximum-likelihood-estimation](./maximum-likelihood-estimation.md) rather than [[ordinary-least-squares]]

The logistic regression is an example of a [[generalised-linear-model]].