A bag-of-words (BoW) representation is a simple way of transforming a text document into a vector of integers. The bag-of-words approach simply counts all occurrences of each word (or other symbol of interest) in the document and produces a vector of those counts.

For example, take the following document:
$$
\text{"dog dog cat dog cat bird dog"}
$$
The bag-of-words approach would then count the occurrences of each word and produce a vector:
$$
[4, 2, 1] \quad \text{in [dog, cat, bird] space}
$$
The dimension of the vector is the vocabulary size.

These vectors can then be passed on to a classifier or other machine learning algorithm to make predictions on the document. However, this old-school method for document classification is limited:
- Words are modelled independently of each
- The meaning of the words are not considered, only whether they appear or not
- One cannot easily reuse the knowledge gained from this model in other settings