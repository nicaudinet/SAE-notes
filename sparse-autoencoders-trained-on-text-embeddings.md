This page aims to gather a few papers which train [SAEs](./SAE-sparse-autoencoders.md) on the output of text embedding models, specifically.

[Disentangling Dense Embeddings](./disentangling-dense-embeddings-with-sparse-autoencoders.md) is the first work to train SAEs on text embeddings. They train them on 420K scientific paper abstracts, analyse the resulting features, and show that they can be used to aid semantic search.

[HypotheSAE](./HypotheSAE-sparse-autoencoders-for-hypothesis-generation.md) uses SAE and a logistic regression head to identify features relevant to a target variable, and then treat explanations generated from the features as hypotheses for how the classifier works.

[LangSAE](./LangSAE-Editing-improving-multilingual-information-retrieval-via-post-hoc-language-identity-removal.md) uses SAEs to identify and mask features which contain language-identity information to improve retrieval (otherwise documents with the same language as the query have an unwanted advantage).
