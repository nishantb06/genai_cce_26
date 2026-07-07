The difficulty of a countably infinite set is that there are infinitely many subsets in the [[Field]] of a countably infinite set. Having a finite union and a finite intersection is insufficient to ensure the closedness of all intersections and unions. In particular, having $F_1 \cup F_2 \in \mathcal{F}$ does not automatically give us $\bigcup_{n=1}^{\infty} F_n \in \mathcal{F}$ because the latter is an infinite union. Therefore, for countably infinite sets, the requirements on an [[Event space]] are more restrictive than for a plain [[Field]]: we need closure under countable intersection and union. The resulting collection is called a **σ-field** (the same object as a [[Sigma Algebra|σ-algebra]]).

A σ-field $\mathcal{F}$ is a [[Field]] such that:

- $\mathcal{F}$ is a [[Field]], and
- if $F_1, F_2, \ldots \in \mathcal{F}$, then the union $\bigcup_{i=1}^{\infty} F_i$ and the intersection $\bigcap_{i=1}^{\infty} F_i$ are both in $\mathcal{F}$.

When do we need a σ-field? When the [[Sample space]] $\Omega$ is countable and has infinitely many elements. For example, if $\Omega$ contains all integers, then the collection of all possible subsets is a σ-field. For another example, if $E_1 = \{2\}$, $E_2 = \{4\}$, $E_3 = \{6\}$, $\ldots$, then $\bigcup_{n=1}^{\infty} E_n = \{2, 4, 6, 8, \ldots\}$ (the positive even numbers). Clearly, we want $\bigcup_{n=1}^{\infty} E_n$ to live in the [[Event space]] $\mathcal{F}$ — not just in $\Omega$.
