Natural 
==Natural Direct Effect== (NDE): How would $Y$ be affected by a change in $T$, but without the mediator $M$ changing due to $T$?
```tikz
\usetikzlibrary{arrows, arrows.meta} % Used for arrow heads
\usetikzlibrary{positioning} % Used for below =of t type commands
\begin{document}
\begin{tikzpicture}[
	node distance = 2cm,
	% Arrow head
	-Latex,
	% Set lines to thick
	thick,
	% Observed variable
	state/.style = {circle, draw, minimum width = 1 cm},
]
	\node[state] (t) at (0,0) {$T$};
	\node[state] (m) [above right= of t] {$M$};
	\node[state] (y) [below right= of m] {$Y$};
	\path (t) edge (m);
	\path[color=red, line width=2] (t) edge (y);
	\path (m) edge (y);
\end{tikzpicture}
\end{document}
```
$$
NDE := \E[Y(1,M(0)) - Y(0,M(0))]
$$

Example: what happens when nicotine is kept at non-smoking levels, but we start smoking?

==Natural Indirect Effect== (NIE): How would $Y$ be affected by $M$ caused by a change in in $T$, but without $T$ changing?
```tikz
\usetikzlibrary{arrows, arrows.meta} % Used for arrow heads
\usetikzlibrary{positioning} % Used for below =of t type commands
\begin{document}
\begin{tikzpicture}[
	node distance = 2cm,
	% Arrow head
	-Latex,
	% Set lines to thick
	thick,
	% Observed variable
	state/.style = {circle, draw, minimum width = 1 cm},
]
	\node[state] (t) at (0,0) {$T$};
	\node[state] (m) [above right= of t] {$M$};
	\node[state] (y) [below right= of m] {$Y$};
	\path[color=black!30!green, line width=2] (t) edge (m);
	\path (t) edge (y);
	\path[color=black!30!green, line width=2] (m) edge (y);
\end{tikzpicture}
\end{document}
```
$$
NIE := \E[Y(0,M(1)) - Y(0,M(0))]
$$

$$
Y(t,m) \perp M(t') \mid X
$$

Under these assumptions, we can decompose the ==total effect== (TE) as:
$$
TE = NDE - NIE_r
$$
where $NIE_r$ is the **reverse natural indirect effect**:
$$
NIE_r = \E[Y(0,M(0)) - Y(0, M(1))]
$$