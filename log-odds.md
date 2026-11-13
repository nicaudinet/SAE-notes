It's annoying to compare [odds](./odds.md) directly, because they are not symmetric around 1. The odds of losing 1:5 are $\frac{1}{5} = 0.2$, but the odds of winning 5:1 are $\frac{5}{1} = 5$, which is much further away from 1

```tikz
\usetikzlibrary{arrows, arrows.meta}
\begin{document}
\begin{tikzpicture}[very thick]

\draw[->] (0,0) -- (12,0);
\foreach \i in {0,1,2,3,4,5} {
    \draw[-] (2*\i,-0.1) -- (2*\i,0.1);
    \node (\i) at (2*\i, -0.4) {\i};
}

\draw[<->, color=red] (0.4,0.25) -- (2,0.25);
\node[red] (lose) at (1.2,0.7) {\Large 1:5};

\draw[<->, color=blue] (2,0.25) -- (10,0.25);
\node[blue] (win) at (6,0.7) {\Large 5:1};

\end{tikzpicture}
\end{document}
```

People solve this with the log odds:
$$
\ln \frac{1}{5} = -\ln 5 = -1.61
$$
$$
\ln \frac{5}{1} = \ln 5 = 1.61
$$

```tikz
\usetikzlibrary{arrows, arrows.meta}
\begin{document}
\begin{tikzpicture}[very thick]

\draw[<->] (0,0) -- (12,0);
\foreach \i in {-2,-1,0,1,2} {
    \draw[-] (6+2*\i,-0.1) -- (6+2*\i,0.1);
    \node (\i) at (6+2*\i, -0.4) {\i};
}

\draw[<->, color=red] (6 - 2 * 1.61, 0.25) -- (6, 0.25);
\node[red] (lose) at (6 - 1.61, 0.7) {\Large 1:5};

\draw[<->, color=blue] (6, 0.25) -- (6 + 2 * 1.61, 0.25);
\node[blue] (win) at (6 + 1.61, 0.7) {\Large 5:1};

\end{tikzpicture}
\end{document}
```