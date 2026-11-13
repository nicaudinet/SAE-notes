Here's the proof for Proposition 3.1 from the [HypotheSAE paper](./HypotheSAE-sparse-autoencoders-for-hypothesis-generation.md) (from Appendix F).

Let
- $p_{ab} := P(\hat Z = a, Z = b)$
- $y_{ab} := \E[Y \mid \hat Z = a, Z = b]$

By the law of total expectation
$$
\E[Y \mid \hat Z = 1] = \frac{y_{11} p_{11} + y_{10} p_{10}}{p_{11} + p_{10}}
\qquad \text{and} \qquad
\E[Y \mid Z = 1] = \frac{y_{11} p_{11} + y_{01} p_{01}}{p_{11} + p_{01}}
$$

Therefore
$$
\begin{align}
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
& = \frac{y_{11} p_{11} + y_{10} p_{10}}{p_{11} + p_{10}}
- \frac{y_{11} p_{11} + y_{01} p_{01}}{p_{11} + p_{01}} \\
& = y_{11} \left( \frac{p_{11}}{p_{11} + p_{10}} - \frac{p_{11}}{p_{11} + p_{01}} \right)
+ \frac{y_{10} p_{10}}{p_{11} + p_{10}}
- \frac{y_{01} p_{01}}{p_{11} + p_{01}} \\
\end{align}
$$

Since
$$
\frac{p_{11}}{p_{11} + p_{10}} = 1 - \frac{p_{10}}{p_{11} + p_{10}}
$$
and similarly
$$
\frac{p_{11}}{p_{11} + p_{01}} = 1 - \frac{p_{01}}{p_{11} + p_{01}}
$$
then
$$
\frac{p_{11}}{p_{11} + p_{10}} - \frac{p_{11}}{p_{11} + p_{01}}
= \left( 1 - \frac{p_{10}}{p_{11} + p_{10}} \right)
- \left( 1 - \frac{p_{01}}{p_{11} + p_{01}} \right)
= \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}}
$$
and therefore
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
= y_{11} \left( \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \right)
+ \frac{y_{10} p_{10}}{p_{11} + p_{10}}
- \frac{y_{01} p_{01}}{p_{11} + p_{01}}
$$

Next, we find the upper bound.

Since $y_{10} \leq 1$ and $y_{01} \geq 0$ then
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\leq y_{11} \left( \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \right)
+ \frac{p_{10}}{p_{11} + p_{10}}
$$

If
$$
\frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \geq 0
$$
then since $y_{11} \leq 1$
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\leq \left( \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \right)
+ \frac{p_{10}}{p_{11} + p_{10}}
= \frac{p_{01}}{p_{11} + p_{01}}
$$
else
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\leq \frac{p_{10}}{p_{11} + p_{10}}
$$

Therefore, combining the two we get the upper bound
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\leq \max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right)
$$

Moving on, we can apply the same logic to find the lower bound.

Since $y_{10} \geq 0$ and $y_{01} \leq 1$ then
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\geq
y_{11} \left( \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \right) - \frac{p_{01}}{p_{11} + p_{01}}
$$

If
$$
\frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \leq 0
$$
then since $y_{11} \leq 1$
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\geq
\left( \frac{p_{01}}{p_{11} + p_{01}} - \frac{p_{10}}{p_{11} + p_{10}} \right) - \frac{p_{01}}{p_{11} + p_{01}}
= - \frac{p_{10}}{p_{11} + p_{10}}
$$
else
$$
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
\geq
- \frac{p_{01}}{p_{11} + p_{01}}
$$

Therefore, combining the two we get the lower bound
$$
\begin{align}
\E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1]
& \geq \min \left( -\frac{p_{10}}{p_{11} + p_{10}}, -\frac{p_{01}}{p_{11} + p_{01}} \right) \\
& \geq - \max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right) \\
\end{align}
$$

The upper and lower bounds can be combined into the absolute-value bound
$$
| \E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1] |
\leq \max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right)
$$
and the same logic applies to $| \E[Y \mid \hat Z = 0] - \E[Y \mid Z=0] |$
$$
| \E[Y \mid \hat Z = 0] - \E[Y \mid Z=0] |
\leq \max \left( \frac{p_{10}}{p_{00} + p_{10}}, \frac{p_{01}}{p_{00} + p_{01}} \right)
$$

Next, notice that
$$
\frac{p_{10}}{p_{00} + p_{10}}
= \frac{p_{10}}{p_{11} + p_{10}} \cdot \frac{p_{11} + p_{10}}{p_{00} + p_{10}}
= \frac{p_{10}}{p_{11} + p_{10}} \cdot \frac{P(\hat Z = 1)}{P(Z=0)}
$$
and that similarly
$$
\frac{p_{01}}{p_{00} + p_{01}}
= \frac{p_{01}}{p_{11} + p_{01}} \cdot \frac{p_{11} + p_{01}}{p_{00} + p_{01}}
= \frac{p_{01}}{p_{11} + p_{01}} \cdot \frac{P(Z = 1)}{P(\hat Z=0)}
$$

Let
$$
p := \min(P(\hat Z = 0), P(Z = 0))
$$
then
$$
P(\hat Z = 0), P(Z = 0) \geq p \qquad \text{and} \qquad P(\hat Z = 1), P(Z = 1) \geq 1 - p
$$
and therefore
$$
\frac{P(\hat Z = 1)}{P(Z = 0)}, \frac{P(Z = 1)}{P(\hat Z = 1)} \leq \frac{1 - p}{p}
$$

Let
$$
M := \max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right)
$$
then
$$
\begin{align}
\max \left( \frac{p_{10}}{p_{00} + p_{10}}, \frac{p_{01}}{p_{00} + p_{01}} \right)
& = \max \left( \frac{p_{10}}{p_{11} + p_{10}} \cdot \frac{P(\hat Z=1)}{P(Z=0)}, \frac{p_{01}}{p_{11} + p_{01}} \cdot \frac{P(Z=1)}{P(\hat Z = 0)} \right) \\
& \leq \max \left( \frac{p_{10}}{p_{11} + p_{10}} \cdot \frac{1 - p}{p}, \frac{p_{01}}{p_{11} + p_{01}} \cdot \frac{1 - p}{p} \right) \\
& = \frac{1 - p}{p} \max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right) \\
\end{align}
$$
and therefore
$$
| \E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1] | \leq M
$$
and
$$
| \E[Y \mid \hat Z = 0] - \E[Y \mid Z=0] |
\leq \frac{1-p}{p} M
$$

Now we're finally ready to tackle the main proof.
$$
\begin{align}
| S(\hat Z) - S(Z) |
& = | | \E[Y \mid \hat Z = 1] - \E[Y \mid \hat Z = 0] | - | \E[Y \mid Z = 1] - \E[Y \mid Z = 0] | | \\
& \leq | ( \E[Y \mid \hat Z = 1] - \E[Y \mid \hat Z = 0] ) - ( \E[Y \mid Z = 1] - \E[Y \mid Z = 0] ) | \\
& = | ( \E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1] ) - ( \E[Y \mid \hat Z = 0] - \E[Y \mid Z = 0] ) | \\
& \leq | \E[Y \mid \hat Z = 1] - \E[Y \mid Z = 1] | + | \E[Y \mid \hat Z = 0] - \E[Y \mid Z = 0] ) | \\
& \leq M + \frac{1 - p}{p}M \\
& = M \left( 1 + \frac{1 - p}{p} \right) \\
& = \frac{1}{p} M
\end{align}
$$
where
- used the inverse triangle inequality $||A| - |B|| \leq |A - B|$ in the second line
- used the triangle inequality $|A - B| \leq |A| + |B|$ in the fourth line

$\text{precision}$ is the probability that the neuron fires ($Z=1$) when the concept is present ($\hat Z = 1$):
$$
\text{precision} = \frac{p_{11}}{p_{11} + p_{10}} = 1 - \frac{p_{10}}{p_{11} + p_{10}}
$$

$\text{recall}$ is the probability that the concept is present ($\hat Z=1$) when the neuron fires ($Z=1$):
$$
\text{recall} = \frac{p_{11}}{p_{11} + p_{01}} = 1 - \frac{p_{01}}{p_{11} + p_{01}}
$$

Therefore
$$
\begin{align}
\max \left( \frac{p_{10}}{p_{11} + p_{10}}, \frac{p_{01}}{p_{11} + p_{01}} \right)
& = \max \left( 1 - \text{precision}, 1 - \text{recall} \right) \\
& = - \min \left( \text{precision} - 1, \text{recall} - 1 \right) \\
& = 1 - \min \left( \text{precision}, \text{recall} \right) \\
\end{align}
$$

And finally:
$$
| S(\hat Z) - S(Z) | \leq \frac{1 - \min(\text{precision}, \text{recall})}{\min(P(\hat Z = 0), p(Z = 0))} = \delta(\hat Z, Z)
$$

QED