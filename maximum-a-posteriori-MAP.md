Maximum A Posteriori (MAP) is a way of estimating the parameters of an assumed probability distribution given some data.

However, unlike [MLE](./maximum-likelihood-estimation.md), it takes a [bayesian perspective](./bayes-theorem.md) by considering a prior and maximising the posterior. In other words, given some data $D$ then
$$
\theta_\text{MAP}
= \underset{\theta}{\text{argmax}} P(\theta \mid D)
= \underset{\theta}{\text{argmax}} P(D \mid \theta) P(\theta)
$$
where the $P(D)$ term from the Bayes formula is dropped because it does not affect the outcome of the $\text{argmax}$.

MLE is a special case of MAP when one uses a uniform prior.

You can also take the $\log$ within the $\text{argmax}$ and get the same result since $\log$ is a monotonically increasing function. This helps simplify the equation:
$$
\theta_\text{MAP}
= \underset{\theta}{\text{argmax}} [ \log P(D \mid \theta)) + \log P(\theta) ]
$$

# Gaussian Prior
Set a [[normal-distribution|Gaussian]] prior on $\theta$ gives you [L2 regularisation](./vector-norms.md).

Assume that the prior is normally distributed:
$$
P(\theta)
= \frac{1}{\sqrt{2 \pi \sigma^2}} \exp \left( \frac{-(\theta - \mu)^2}{2 \sigma ^2} \right)
$$

then, taking the log:
$$
\log P(\theta) \\
= \underbrace{\log \left( \frac{1}{\sqrt{2 \pi \sigma^2}} \right)}_{\text{constant w.r.t. } \theta} - \frac{(\theta - \mu)^2}{2 \sigma ^2}
= - \frac{(\theta - \mu)^2}{2 \sigma ^2}
$$

setting $\mu = 0$ and $\sigma = 1$ for simplicity, the MAP estimate becomes:
$$
\theta_\text{MAP}
= \underset{\theta}{\text{argmax}} [ \log P(D \mid \theta)) - \theta^2 ]
$$
which is L2 regularisation.