Here's the [paper](./the-linear-representation-hypothesis-and-the-geometry-of-large-language-models.md) that formalises the [linear representation hypothesis](./linear-representation-hypothesis.md).

Here's another [paper](./a-survey-on-the-linear-representation-hypothesis.md) which takes this formalisation further and makes it scientifically falsifiable. 

# Motivation

Empirically, linear probes can accurately predict the presence of complex concepts from activations.

Modifying activations along linear directions can systematically change model behaviour. Linear directions are not just correlated with concepts. 

[SAEs](./SAE-sparse-autoencoders.md) recover interpretable concepts (some of the time).

[Some theoretical evidence](./on-the-origins-of-linear-representations-in-language-models.md) also.

# Pushback

[This paper](./is-a-linear-probe-evidence-of-a-linear-representation%3F.md) argues that linear probes are not enough evidence for linearity. In particular, they argue that high linear probe accuracy could be due to:
1) a true linear world model where the latent-aligned subspace dominates, or
2) a kernel machine where the latents lie linearly inside a much larger curved manifold

Steering directions may be affecting multiple concepts at the same time.


