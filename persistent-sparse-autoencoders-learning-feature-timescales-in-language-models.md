---
tags:
  - paper
---
https://arxiv.org/pdf/2607.17117

---

Standard [SAEs](./SAE-sparse-autoencoders.md) encode each token independently. Information that persists along a sequence is therefore lost.

This paper introduces ==Persistent SAEs== which learn a persistence coefficient for each feature. They show that they can maintain competitive reconstruction while learning features with a bunch of different "speeds". Fast features tend to be locally interpretable detectors. Slow features tend to be compact semantic states that retain topic-level information.