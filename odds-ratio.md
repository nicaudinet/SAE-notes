The odds ratio is a ratio of [odds](./odds.md). If we take two odds of 5:2 and 3:4, then their odds ratio is:
$$
OR = \frac{5/2}{3/4} = \frac{10}{3} = 3.33
$$
Like with normal odds:
- If $0 < OR < 1$: the odds on top is smaller than the odds on the bottom
- If $OR = 1$: the odds are the same
- If $1 < OR$: the odds on top is larger than the odds on the bottom

Also like with [log-odds](./log-odds.md), taking the log of the odds ratio makes everything symmetric around 0

Like $R^2$, the odds ration can show a relationship between two things. For example, imagine we ask whether having a mutated gene affects your odds of getting cancer. We collect the following data:
```tikz
\usetikzlibrary{arrows, arrows.meta}
\begin{document}
\begin{tikzpicture}[thick]

\draw[-] (0,0) -- (0,4);
\draw[-] (2,0) -- (2,4);
\draw[-] (4,0) -- (4,4);
\draw[-] (0,0) -- (4,0);
\draw[-] (0,2) -- (4,2);
\draw[-] (0,4) -- (4,4);

\node (tl) at (1,3) {\Large 23};
\node (tr) at (3,3) {\Large 117};
\node (bl) at (1,1) {\Large 6};
\node (br) at (3,1) {\Large 210};

\node (a) at (1,4.5) {\Large Yes};
\node (b) at (3,4.5) {\Large No};
\node (d) at (-0.5,3) {\Large Yes};
\node (c) at (-0.5,1) {\Large No};

\node (cancer) at (2,5.5) {\Large Has Cancer};
\node[rotate=90, align=center] (p) at (-1.5,2) {\Large Has Mutated Gene};

\end{tikzpicture}
\end{document}
```
Then the odds ratio is:
$$
OR = \frac{23/117}{6/210} = \frac{0.2}{0.03} = 6.88
$$
Therefore having a mutated gene is a good predictor for having cancer. More broadly:
- The larger the odds ratio, the more positive relationship there is between having a mutated gene and cancer
- The closer the odds ratio is to 1, the less of a relationship there is between the two variables
- The closer the odds ratio is to 0, the more of a negative relationship there is between having a mutated gene and cancer
## General formula

Let $A \in \{0,1\}$ and $B \in \{0,1\}$. The odds ratio of $A$ and $B$ is the ratio of the odds of $A$ taking place in the presence of $B$ and $A$ taking place in the absence of $B$:
$$
OR = \frac{P(A=1 \mid B=1)/P(A=0 \mid B=1)}{P(A=1 \mid B=0)/P(A=0 \mid B=0)}
$$
Two events are independent if they have an odds ratio of 1, meaning that $A$ has the same odds regardless of whether $B$ is present of not

One way to generalise the odds ratio is [logistic-regression](./logistic-regression.md)

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/8nm0G-1uJzA?si=XcOzzECsaVZVUW4K" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>