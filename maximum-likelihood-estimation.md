Maximum Likelihood Estimation (MLE) is a way of estimating the parameters of an assumed probability distribution given some data.

MLE works by maximising a [likelihood function](./likelihood-function.md) to find the parameters which are the most likely to have generated the observed data. In other words, given some data $D$ it performs:
$$
\theta_\text{MLE} = \arg\max_\theta P(D \mid \theta)
$$