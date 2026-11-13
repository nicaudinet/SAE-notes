
```tikz
\usetikzlibrary{positioning}
\usetikzlibrary{backgrounds}

\begin{document}

\begin{tikzpicture}[
    neuron/.style={
        circle,
        draw=black!65,
        fill=white,
        minimum size=5mm,
        inner sep=0pt,
        line width=1pt,
    },
    active/.style={
        neuron,
        fill=blue!55,
        draw=blue!70!black
    },
    connection/.style={
        draw=black!30,
        line width=0.7pt
    }
]

% Layer positions
\def\xInput{0}
\def\xLatent{3.5}
\def\xOutput{7}

% Connections first (behind nodes)
\foreach \i in {1,...,5} {
    \foreach \j in {1,...,8} {
        \draw[connection]
            (\xInput,{(3-\i)*0.85}) --
            (\xLatent,{(4.5-\j)*0.75});

        \draw[connection]
            (\xLatent,{(4.5-\j)*0.75}) --
            (\xOutput,{(3-\i)*0.85});
    }
}

% Input and output nodes
\foreach \i in {1,...,5} {
    \node[neuron] at
        (\xInput,{(3-\i)*0.85}) {};

    \node[neuron] at
        (\xOutput,{(3-\i)*0.85}) {};
}

% Sparse latent nodes
\foreach \j in {1,...,8} {
    \ifnum\j=2
        \node[active] at
            (\xLatent,{(4.5-\j)*0.75}) {};
    \else
        \ifnum\j=6
            \node[active] at
                (\xLatent,{(4.5-\j)*0.75}) {};
        \else
            \node[neuron] at
                (\xLatent,{(4.5-\j)*0.75}) {};
        \fi
    \fi
}

% Encoder / Decoder labels
\node at (1.75,3.4) {\Large Encoder};
\node at (5.25,3.4) {\Large Decoder};

% Layer labels
\node[align=center] at (0,-3.5) {Input \\ ($\textbf x$)};
\node[align=center] at (3.5,-3.5) {Sparse features \\ ($\textbf z$)};
\node[align=center] at (7,-3.5) {Reconstruction \\ ($\hat{\textbf x}$)};

\end{tikzpicture}

\end{document}
```

Sparse AutoEncoders (SAEs) are an unsupervised method for learning interpretable latent features in neural networks.

SAEs are usually structured as follows. Given an input activation $\textbf x \in \R^d$:
$$
\begin{align}
\textbf z &= \text{ReLU}(W_\text{enc} \textbf x + \textbf b_\text{enc}) \\
\hat{\textbf x} &= W_\text{dec} \textbf z + \textbf b_\text{dec}
\end{align}
$$

SAEs are trained to both minimise the squared error $\| \textbf{x} - \hat{\textbf{x}} \|_2^2$ and for sparsity of feature activations ($L_1$ loss):
$$
\mathcal{L}(\textbf x) = \| \textbf x - \hat{\textbf x} \|_2^2 + \alpha \| \textbf z \|_1
$$

The motivation for SAEs rests on three hypotheses:
1) The [Linear Representation Hypothesis](./linear-representation-hypothesis.md)
2) The [Superposition Hypothesis](./superposition-hypothesis.md)
3) The [Sparsity Hypothesis](./sparsity-hypothesis.md)

SAEs are a popular tool in the [mechanistic interpretability](./mechanistic-interpretability.md) community and have found several [use cases](./SAE-use-cases.md). They were formally introduced in [this paper](./sparse-autoencoders-find-highly-interpretable-features-in-language-models.md) but also popularised by [this](./toy-models-of-superposition.md) and [this](./towards-monosemanticity.md) blog post from Anthropic.

SAE features are often interpreted with an [autointerp pipeline](./SAE-feature-interpretation.md).

SAEs have several known [failure modes](./SAE-failure-modes.md).

There are [many SAE variants](./sparse-autoencoder-variants.md) to address them.

SAEs are related to [transcoders](./transcoder.md).