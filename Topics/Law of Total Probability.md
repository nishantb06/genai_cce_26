Let $\{A_1, \ldots, A_n\}$ be a partition of $\Omega$, i.e., $A_1, \ldots, A_n$ are disjoint and $\Omega = A_1 \cup \cdots \cup A_n$. Then, for any $B \subseteq \Omega$,

$$P(B) = \sum_{i=1}^{n} P(B \mid A_i)\, P(A_i).$$

**Proof.** We start from the right-hand side.

$$
\begin{aligned}
\sum_{i=1}^{n} P(B \mid A_i)\, P(A_i)
&= \sum_{i=1}^{n} P(B \cap A_i) && \text{(a)} \\
&= P\!\left(\bigcup_{i=1}^{n} (B \cap A_i)\right) && \text{(b)} \\
&= P\!\left(B \cap \left(\bigcup_{i=1}^{n} A_i\right)\right) && \text{(c)} \\
&= P(B \cap \Omega) = P(B), && \text{(d)}
\end{aligned}
$$

where (a) follows from the definition of conditional probability, (b) is due to Axiom III, (c) holds because of the distributive property of sets, and (d) results from the partition property of $\{A_1, A_2, \ldots, A_n\}$.
