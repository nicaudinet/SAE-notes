---
tags:
  - dataset
---
https://huggingface.co/datasets/charlieoneill/medical-qa-combined

A dataset of medical QA examples taken from several different existing medial QA datasets. It was used in the [Resurrecting the Salmon](./resurrecting-the-salmon-rethinking-mechanistic-interpretability-with-domain-specific-sparse-autoencoders.md) paper to train domain-specific [SAEs](./SAE-sparse-autoencoders.md).

For each example they concatenate the question, multiple choice options, correct answer, and any other details into a single string. In total this amounted to ~200K examples and ~50M tokens.
