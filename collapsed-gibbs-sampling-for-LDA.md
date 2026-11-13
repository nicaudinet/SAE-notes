Collapsed Gibbs sampling is a Markov chain Monte Carlo method for approximately sampling an [lda-model](./lda-model.md). It is "collapsed" because both the $\theta$ and the $\phi$ are integrated out to make the algorithm more efficient. This way we only need to sample the per-word topic assignments $z_{d,n}$ from which we can then compute $\theta_d$ and $\phi_k$.

Algorithm:
1) Randomly assign a topic to every word in the corpus
2) Count the number of times topic $k$ occurs in each document $d$
3) Count the number of times word $w_{d,n}$ is assigned to topic $k$ in the corpus
4) In a document, un-assign a word from its topic and remove the word from the tables computed in step 2) and 3)
5) Assign the word to a new topic based on:
	1) How prevalent the topic is in document $d$
	2) How prevalent the word is in topic $k$
6) Repeat steps 2)-5) for every word in every document in the corpus. This is one iteration
7) Repeat step 6) for as many iterations as required
8) Extract $\theta_d$ and $\phi_k$ from the per-word topic assignments $z_{d,n}$

The prevalence of a topic in a document is given by the following, where $n_{d,k}$ is the number of words in document $d$ assigned to topic $k$:
$$
\frac{n_{d,k} + \alpha}{\sum_{i=1}^K n_{d,i} + K \alpha}
$$

The prevalence of a word in a topic is given by the following, where $m_{k,w}$ is the number of times the word $w$ was  assigned to topic $k$ in the corpus:
$$
\frac{m_{k,w} + \beta}{\sum_{i=1}^V m_{k,i} + V \beta}
$$