Word embedding or word representation models are language models that transform words to vectors.
$$
\huge{\text{word} \rightarrow \mathbb{R}^D}
$$

In order to perform computation on text, computers need to transform human-understandable words into representations that the computers can understand. The most common word representation are These are usually vectors of real numbers. The size of the vector, $D$ is the ==embedding dimention==. Larger embedding dimensions allow models to capture more information about the words but are more difficult to train.

Ideally, the vector embedding of the words capture semantic information about the words, where words embedded close to each other in the vector space are similar in some way. A common measure of distance is the 

The simplest

[bag-of-words-representation](./bag-of-words-representation.md)
[tf-idf-word-embedding](./tf-idf-word-embedding.md)

[word2vec](./word2vec.md)
[GloVe](./GloVe.md)

[BERT-models](./BERT-models.md)