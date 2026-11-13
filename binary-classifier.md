A binary classifier is a model $f$ which maps inputs from some input space $\mathcal{I}$ into a binary variable:
$$
f : \mathcal{I} \r \mathbb{B}
$$
In other words, a binary classifier predicts whether a sample should be classified as "positive" (belongs to the class) or "negative" (does not belong to the class). This produces one of four outcomes:

```tikz
\usetikzlibrary{positioning} % Used for below =of t type commands
\usetikzlibrary{calc} % Used for coordinate calculations
\begin{document}
\begin{tikzpicture}[
    node distance = 0cm,
	box/.style =
    	{ rectangle
    	, draw
    	, minimum width = 2.5 cm
    	, minimum height = 2.5 cm
    	, align = center
    	},
]

\node[box, fill = green!20!white] (tp) at (0,0) {True Positive \\ (TP)};
\node[box, fill = red!20!white] (fp) [right= of tp] {False Positive \\ (FP)};
\node[box, fill = red!20!white] (fn) [below= of tp] {False Negative \\ (FN)};
\node[box, fill = green!20!white] (tn) [right= of fn] {True Negative \\ (TN)};

\node (ground-truth) at ($(tp)!0.5!(fp) + (0,2.2)$) {Ground-Truth};
\node (gt) [above=0.1cm of tp] {true};
\node (gn) [above=0.1cm of fp] {false};

\node (predicted) at ($(tp)!0.5!(fn) + (-2.2,0)$) {\rotatebox{90}{Predicted}};
\node (pt) [left=0.1cm of tp] {\rotatebox{90}{true}};
\node (pn) [left=0.1cm of fn] {\rotatebox{90}{false}};
 
\end{tikzpicture}
\end{document}
```

A classic example of a binary classifier is the binary [logistic-regression](./logistic-regression.md).