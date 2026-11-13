# TF-IDF Embedding

==Term Frequency==: frequency of a given word in a document. Words with higher frequencies deemed more important. Defined as:
$$
TF(w,d) = \frac{\text{\# times word $w$ appears in document $d$}}{\text{\# words in document $d$}}
$$

==Inverse Document Frequency==: measure how often a word appears in documents in the corpus. Words that appear in fewer documents deemed more important. Defined as:
$$
IDF(w,D) = ln \left( \frac{\text{\# documents in corpus $D$}}{\text{\# of documents containing word $w$}} \right)
$$

These two measures are combined to form ==TF-IDF weights== $W$:
$$
W(w,d,D) = TF(w,d) \times IDF(w,D)
$$
These weights measure how important each word is in documents. Words that appear often but only in few documents will be given high weights. Words that appear frequently in many documents are given low weights (removes common words like "a", "the", "is").

To form the TF-IDF word embedding, the weights $W$ are combined with a notion of word proximity. Let $V = \{v_1, \ldots v_V\}$ be the vocabulary for corpus $D$. Let $n(w,i,d; k)$ be the number of times that word $v_i$ appears within distance $k$ of word $w$ in document $d$. Then, the ==TF-IDF embedding== for a particular word $w$ is given by:
$$
Emb(w) = (n_1, \ldots, n_V) \quad \text{where} \quad n_i = \sum_{d=1}^D W(w,d,D) \times n(w,i,d;k)
$$
