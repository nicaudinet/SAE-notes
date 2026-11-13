---
tags:
  - paper
---
https://arxiv.org/pdf/2610.22655

---

We usually argue for the [linear representation hypothesis](./linear-representation-hypothesis.md) by training a linear probe and seeing if the accuracy is high. They argue in this paper that this test is too permissive.

High linear probe accuracy could be due to:
1) a true linear world model where the latent-aligned subspace dominates, or
2) a kernel machine where the latents lie linearly inside a much larger curved manifold

Imagine two models representing the 2D position of an object $x$.

In a true linear world model, the representation directly represents the 2D coordinates:
$$
f(x) = [z_1, z_2]
$$

In a kernel machine, though, the representation could be a huge number of complicated non-linear features (the much larger curved manifold):
$$
f(x) = [\sin(z_1), \cos(z_1), z_2^2, \ldots]
$$
It turns out that with just a linear combination of sufficiently diverse nonlinear features you can approximate almost any reasonably smooth function. The features don't need to be learned, they can be randomly generated.

In the true world model case the position explains all of the structure in the representation. In the kernel machine though the position explains very little of the structure of the representation. Therefore they propose ==reverse predictivity==: rather than asking whether the representation can predict the position, ask whether the position can predict the representation!

Another similar approach they propose is ==spectral concentration==: the two leading directions of the representation (e.g. from [PCA](./principal-component-analysis-PCA.md)) should closely correspond to position in the true linear world model. This is unlikely to happen in the kernel machine case.

Finally, they propose ==out-of-distribution (OOD) generalisation== as a test: kernel machine representations are likely to be more brittle than true linear world models, and therefore are more likely to generalise poorly on OOD samples. Sufficiently rich kernel machines can also generalise well though, so good OOD generalisation is not proof by itself. 