# LDA model

```tikz

% From https://github.com/jluttine/tikz-bayesnet/blob/master/README.rst

\usetikzlibrary{shapes}
\usetikzlibrary{fit}
\usetikzlibrary{chains}
\usetikzlibrary{arrows}

\begin{document}
\begin{tikzpicture}

% Latent node
\tikzstyle{latent} = [
	circle,
	fill=white,
	draw=black,
	inner sep=1pt,
	minimum size=20pt,
	font=\fontsize{10}{10}\selectfont,
	node distance=2
]

% Observed node
\tikzstyle{obs} = [latent, fill=gray!25]

% Constant node
\tikzstyle{const} = [rectangle, inner sep=0pt, node distance=2]

% Factor node
\tikzstyle{factor} = [
	rectangle,
	fill=black,
	minimum size=5pt,
	inner sep=0pt,
	node distance=0.8
]

% Deterministic node
\tikzstyle{det} = [latent, diamond]

% Plate node
\tikzstyle{plate} = [draw, rectangle, rounded corners, fit=#1]
% Invisible wrapper node
\tikzstyle{wrap} = [inner sep=0pt, fit=#1]
% Gate
\tikzstyle{gate} = [draw, rectangle, dashed, fit=#1]

% Caption node
\tikzstyle{caption} = [font=\footnotesize, node distance=0]
\tikzstyle{plate caption} = [
	caption,
	node distance=0,
	inner sep=0pt,
	below right=5pt and 0pt of #1.south east
] %
\tikzstyle{factor caption} = [caption] %
\tikzstyle{every label} += [caption] %

% \factoredge [options] {inputs} {factors} {outputs}
\newcommand{\factoredge}[4][]{ %
  % Connect all nodes #2 to all nodes #4 via all factors #3.
  \foreach \f in {#3} { %
    \foreach \x in {#2} { %
      \path (\x) edge[-,#1] (\f) ; %
      %\draw[-,#1] (\x) edge[-] (\f) ; %
    } ;
    \foreach \y in {#4} { %
      \path (\f) edge[->, >={triangle 45}, #1] (\y) ; %
      %\draw[->,#1] (\f) -- (\y) ; %
    } ;
  } ;
}

% \edge [options] {inputs} {outputs}
\newcommand{\edge}[3][]{ %
  % Connect all nodes #2 to all nodes #3.
  \foreach \x in {#2} { %
    \foreach \y in {#3} { %
      \path (\x) edge [->, >={triangle 45}, #1] (\y) ;%
      %\draw[->,#1] (\x) -- (\y) ;%
    } ;
  } ;
}

% \factor [options] {name} {caption} {inputs} {outputs}
\newcommand{\factor}[5][]{ %
  % Draw the factor node. Use alias to allow empty names.
  \node[factor, label={[name=#2-caption]#3}, name=#2, #1,
  alias=#2-alias] {} ; %
  % Connect all inputs to outputs via this factor
  \factoredge {#4} {#2-alias} {#5} ; %
}

% \plate [options] {name} {fitlist} {caption}
\newcommand{\plate}[4][]{ %
  \node[wrap=#3] (#2-wrap) {}; %
  \node[plate caption=#2-wrap] (#2-caption) {#4}; %
  \node[plate=(#2-wrap)(#2-caption), #1] (#2) {}; %
}

% \gate [options] {name} {fitlist} {inputs}
\newcommand{\gate}[4][]{ %
  \node[gate=#3, name=#2, #1, alias=#2-alias] {}; %
  \foreach \x in {#4} { %
    \draw [-*,thick] (\x) -- (#2-alias); %
  } ;%
}

% \vgate {name} {fitlist-left} {caption-left} {fitlist-right}
% {caption-right} {inputs}
\newcommand{\vgate}[6]{ %
  % Wrap the left and right parts
  \node[wrap=#2] (#1-left) {}; %
  \node[wrap=#4] (#1-right) {}; %
  % Draw the gate
  \node[gate=(#1-left)(#1-right)] (#1) {}; %
  % Add captions
  \node[caption, below left=of #1.north ] (#1-left-caption)
  {#3}; %
  \node[caption, below right=of #1.north ] (#1-right-caption)
  {#5}; %
  % Draw middle separation
  \draw [-, dashed] (#1.north) -- (#1.south); %
  % Draw inputs
  \foreach \x in {#6} { %
    \draw [-*,thick] (\x) -- (#1); %
  } ;%
}

% \hgate {name} {fitlist-top} {caption-top} {fitlist-bottom}
% {caption-bottom} {inputs}
\newcommand{\hgate}[6]{ %
  % Wrap the left and right parts
  \node[wrap=#2] (#1-top) {}; %
  \node[wrap=#4] (#1-bottom) {}; %
  % Draw the gate
  \node[gate=(#1-top)(#1-bottom)] (#1) {}; %
  % Add captions
  \node[caption, above right=of #1.west ] (#1-top-caption)
  {#3}; %
  \node[caption, below right=of #1.west ] (#1-bottom-caption)
  {#5}; %
  % Draw middle separation
  \draw [-, dashed] (#1.west) -- (#1.east); %
  % Draw inputs
  \foreach \x in {#6} { %
    \draw [-*,thick] (\x) -- (#1); %
  } ;%
}

% Nodes
\node[obs] (W) {$W$} ;
\node[latent, left=of W] (Z) {$Z$} ;
\node[latent, left=of Z] (theta) {$\theta$};
\node[const, left=of theta] (alpha) {$\alpha$};

% Factors
\factor[left=of W] {W-f} {below:Multi} {} {} ;
\factor[left=of Z] {Z-f} {above:Multi} {} {} ;
\factor[left=of theta] {theta-f} {above:Dir} {} {} ;

% More nodes
\node[latent, above=of W-f] (phi) {$\phi$};
\node[const, left=of phi] (beta) {$\beta$};

\factor[left=of phi] {phi-f} {above:Dir} {} {} ;

\factoredge {theta} {Z-f} {Z} ;
\factoredge {alpha} {theta-f} {theta} ;
\factoredge {phi} {W-f} {W} ;
\factoredge {beta} {phi-f} {phi} ;

\gate {W-gate} {(W-f)(W-f-caption)} {Z}

\plate
	{plate1}
	{ (W)(W-gate) (Z)(Z-f)(Z-f-caption) }
	{$n = 1 .. N_d$}
	;

\plate
	{}
	{ (plate1) (theta)(theta-f)(theta-f-caption) }
	{$d = 1 .. D$}
	;
 
\plate
	{}
	{ (phi)(phi-f)(phi-f-caption) }
	{$k = 1 .. K$}
	;

\end{tikzpicture}
\end{document}
```

The LDA model is a generative model which creates a corpus of $D$ documents. The model uses a [[dirichlet-distribution]] to sample a per-document topic distribution $\theta_d$ and a per-topic word distribution $\phi_k$. To draw a word in a document, a topic $k$ is first selected from the appropriate $\theta_d$. Then, a word is drawn from the appropriate $\phi_k$ based on the topic draw. This process is repeated for all words in all documents. Each word is drawn independently.

Here is pseudo-code for the algorithm:
1) Fix:
	- the hyper-parameters $\alpha$ and $\beta$ (typically 0.1 or 0.01)
	- the number of topics $K$
	- the number of documents $D$
	- length of each document $N_d$
1) Sample a topic distribution $\theta_d \sim Dir(\alpha)$ for each document $d$
2) Sample a word distribution $\phi_k \sim Dir(\beta)$ for each topic $k$
3) For each pair $(d,n)$ where $n = 1..N_d$:
	1) Sample a topic $z_{d,n} \sim Multi(\theta_d)$
	2) Sample a word $w_{d,n} \sim Multi(\phi_{z_{d,n}})$
where:
- $Dir(x)$ is the Dirichlet distribution
- $Multi(x)$ is the Multinomial distribution
- $N_d$ is the number of words in document $d$

The total probability of the LDA model is:
$$
P(\bm{w}, \bm{z}, \bm{\theta}, \bm{\phi}; \alpha, \beta) = \prod_{k=1}^K P(\phi_k \mid \beta) \prod_{d=1}^D P(\theta_d \mid \alpha) \prod_{n=1}^N P(z_{d,n} \mid \theta_d) P(w_{d,n} \mid \phi_{z_{d,n}})
$$
