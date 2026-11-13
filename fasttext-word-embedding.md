Word embedding based on [word2vec](./word2vec.md) that can deal with morphologically-rich languages.

For example, in Finnish:
$$
\begin{align}
\text{house} &\rightarrow \text{talo} \\
\text{in the house} &\rightarrow \text{talossa} \\
\text{from the house} &\rightarrow \text{talosta} \\
\text{to the house} &\rightarrow \text{taloon} \\
\end{align}
$$

In word2vec these would all be completely independent words. In reality though they are the same word, so we would like their representations to be close in embedding space.

Fasttext uses ==subword information== to achieve this by splitting words into character-level n-grams and then comparing them. This way, if words share a common root (e.g. `talo` in the example above) they will be recognised as similar.

# Links
- [original paper](./enriching-word-vectors-with-subword-information.md)