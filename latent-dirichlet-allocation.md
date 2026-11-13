The goal of Latent Dirichlet Allocation (LDA) is to discover a predefined number of $K$ latent topics in a corpus $D$. Each document is modelled as a mix of topics, and each topic is modelled as a mix of words, taking a [bag-of-words-representation](./bag-of-words-representation.md) approach. LDA then reverse engineers the probability distribution of the topics in each document and the words in each topic by modifying the model parameters until the model can approximately generate the text corpus.

The [lda-model](./lda-model.md) defines each document in a corpus as a mixture of topics, and each topic as a mixture of words from across the corpus. In this way, documents are not treated independently, as topics span the whole corpus. It is a generative model that can be used to sample topics for words in the corpus.
# Learning Topics

In other words, we cant to infer the per-document topic distribution $\theta_d$ and the per-topic word distribution $\phi_k$, but we can only observe  $w_{d,n}$, the words in the corpus. How can we use the LDA model to do this?

The key idea is to train the LDA model to generate the existing corpus by tuning the parameters and then extract $\theta_d$ and $\phi_k$ from the trained model. These distributions are the output of the algorithm, and then need to be interpreted either by humans or automated tagging systems. Many techniques exist to train the LDA model to generate the corpus. One such technique is [collapsed-gibbs-sampling-for-LDA](./collapsed-gibbs-sampling-for-LDA.md), but people also use variational inference for this task. Gibbs sampling techniques tend to be slower but asymptotically more accurate.

# Resources:
- Great explainer video: [automatically-finding-topics-in-documents-with-latent-dirichlet-allocation](./automatically-finding-topics-in-documents-with-latent-dirichlet-allocation.md)
- Blei, David M., Andrew Y. Ng, and Michael I. Jordan. "Latent dirichlet allocation." _Journal of machine Learning research_ 3.Jan (2003): 993-1022. [link to paper](https://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf?ref=https://githubhelp.com)