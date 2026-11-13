---
title: Disentangling Dense Embeddings with Sparse Autoencoders
tags:
  - paper
---
https://arxiv.org/pdf/2408.00657

---

They train [SAEs](./SAE-sparse-autoencoders.md) on text embeddings of 420K scientific paper abstracts from computer science and astronomy.

They use a variant of [TopK SAEs](./topk-sparse-autoencoders.md). They use the same [AuxK loss term](./auxk-loss-term-sparse-autoencoders.md) used by [HypotheSAE](./HypotheSAE-sparse-autoencoders-for-hypothesis-generation.md).

Feature families: related concepts at different levels of abstraction.

They use OpenAI's `text-embedding-3-small` model to generate text embeddings.

They use SAE features to steer semantic search.

They open-source their embeddings, SAEs, and features. Nice!