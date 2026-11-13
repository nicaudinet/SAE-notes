Lewis, Patrick, et al. "Retrieval-augmented generation for knowledge-intensive nlp tasks." _Advances in Neural Information Processing Systems_ 33 (2020): 9459-9474.

- LLMs store facts into their parametric weights
    - Cannot easily expand or revise memory
    - Cannot provide insight into predictions
    - May hallucinate
- With [retrieval-augmented models](./retrieval-augmented-models-RAG.md) one can easily extend and revise the facts and also check what the model accessed to provide a particular answer
- Hybrid parametric and non-parametric memory to seq2seq models
    - Parametric memory: pre-trained seq2seq transformer ([BERT](./BERT-models.md))
    - Non-parametric memory: dense vector index of Wikipedia accessed with pre-trained neural retriever (Dense Passage Retriever (DPR))
- Components combined and trained end-to-end (train both generator and retriever)
    - Retrieved document as latent variable
- Both parametric and non-parametric memories are already pre-trained and pre-loaded with knowledge
- ==Knowledge-intensive tasks==: tasks humans would not reasonably be expected to perform without access to external knowledge

- $x$ - input sequence
- $z$ - retrieved documents
- $y$ - output sequence
- $p_\eta(z \mid x)$ - retriever with parameters $\eta$ which returns top-K truncated distribution over text passages given $x$
- $p_\theta(y_i \mid x, z, y_{1:i-1})$ - auto-regressive generator with parameters $\theta$ which returns next token based on $x$, $z$ and previous output tokens

==Retriever==: based on Deep Passage Retriever (DPR) with bi-encoder architecture:
$$
p_\eta(z \mid x) \propto \exp(d(z)^Tq(x)) \qquad d(z) = \text{BERT}_d(z), \quad q(x) = \text{BERT}_q(x)
$$
- $d(z)$ - dense representation of a document (BERT)
- $q(x)$ - query representation from query encoder (also BERT)
- List of $k$ documents with highest prior probability is a Maximum Inner Product Search (MIPS) problem (can be approximated in sub-linear time) 

==Generator==: based on BERT-large. Input is concatenation of $x$ and $z$

RAG-Sequence: model uses same document to generate every token
$$
p_{RAG-S}(y \mid x) \approx \sum_z p_\eta(z \mid x)p_\theta(y \mid x, z) = \sum_z p_\eta(z \mid x) \prod_i^N p_\theta(y_i \mid x, z, y_{1:i-1})
$$
where $z \in \text{top-K}(p(\cdot \mid x))$.

RAG-Token: model uses different document for each token
$$
p_{RAG-T}(y \mid x) \approx \prod_i^N \sum_z p_\eta(z \mid x) p_\theta(y_i \mid x, z_i, y_{1:i-1})
$$
where $z \in \text{top-K}(p(\cdot \mid x))$.