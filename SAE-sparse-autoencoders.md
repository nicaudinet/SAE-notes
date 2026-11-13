
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

Sparse Autoencoders (SAEs) are an unsupervised method for learning interpretable
features in neural networks.

The modern SAE architecture was academically introduced in [this paper](./sparse-autoencoders-find-highly-interpretable-features-in-language-models.md) and popularised by [this](./toy-models-of-superposition.md) and [this](./towards-monosemanticity.md) blog post from Anthropic.

SAEs are a family of methods rather than a single architecture. That said, they all include an encoder layer which projects the input representation into feature space, and a decoder layer which reconstructs the input from feature space. Encoder and decoder layers are usually linear, with an activation function after the encoder.

The original SAE architecture follows this pattern. Given an input activation $\textbf x \in \R^d$:
$$
\begin{align}
\textbf z &= \text{ReLU}(W_\text{enc} \textbf x + \textbf b_\text{enc}) \\
\hat{\textbf x} &= W_\text{dec} \textbf z + \textbf b_\text{dec}
\end{align}
$$

SAEs are trained to reconstruct the input while activating as few features as
possible. The original SAE does this with a two-part loss function: a reconstruction term which minimises the squared reconstruction error and a sparsity term which minimises the sum of all feature activations ([L1 regularisation](./vector-norms.md)):
$$
\mathcal{L}(\textbf x) = \| \textbf x - \hat{\textbf x} \|_2^2 + \alpha \| \textbf z \|_1
$$

The motivation for SAEs rests on [three hypotheses](./sparse-autoencoder-motivation.md). In brief, SAEs are designed for situations where concepts are linearly encoded in the input representation, concepts are sparse in the training data, and the input directions (neurons) are polysemantic.

SAEs have become a popular tool in the mechanistic interpretability community and have found several [use cases](./SAE-use-cases.md).

SAEs are typically used to analyse or intervene on the internal activations of
language models. There is a branch of research which focuses on training them on
[text embeddings](./sparse-autoencoders-trained-on-text-embeddings.md) which I
find compelling.

Interpreting SAE features can be as challenging as training the SAE themselves. Feature interpretation can be done at scale with an [autointerp pipeline](./SAE-feature-interpretation.md).

SAEs have several known [failure modes](./SAE-failure-modes.md). Researchers have created [many variants](./sparse-autoencoder-variants.md) to mitigate and address these failure modes.

SAEs are related to [transcoders](./transcoder.md).
