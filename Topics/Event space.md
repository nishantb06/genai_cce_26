Set of all subsets of $\Omega$ i.e the [[Sample space]]
The collection of all possible events. An event EE is a subset in ΩΩ that defines an outcome or a combination of outcomes.

Thus, an event can contain one outcome but it can also contain many outcomes.

Denoted by $\mathcal{F}$ 

The second point we should remember is the cardinality of Ω and that of F. A sample space containing n elements has a cardinality n. However, the event space constructed from Ω will contain $2^n$ events. 

- We need $\mathcal{F}$ because the [[Probability measure]] is mapping a set to a number. Probability measure does not take an outcome from [[Sample space]]  but a subset inside [[Event space]]
## Borel sets

A **Borel set** is any subset of the real line (or $\mathbb{R}^n$) that you can build starting from open intervals using only:

- taking complements (everything *not* in the set), and
- taking countable unions or intersections (combining finitely or countably many sets at a time).

In practice: most "nice" subsets you care about in probability — intervals, single points, unions of intervals — are Borel sets. Pathological sets (like Vitali sets) are not.

Formally, the collection of all Borel sets is the smallest [[Sigma Algebra|σ-algebra]] containing every open set. When $\Omega = \mathbb{R}$, we often take the event space to be these Borel sets rather than *all* subsets of $\mathbb{R}$, because not every subset is measurable.


---- 

There are just some basic set operations. We want to ensure that the event space is closed under these set operations. That is, we do not want to be surprised by finding that a set constructed from two events is not an event. However, since all set operations can be constructed from union, intersection and complement, ensuring that the event space is closed under these three operations effectively ensures that it is closed to all set operations. For example the complement of an event should also be an event. The union / intersection of two events should also be an event etc. 

The formal way to guarantee these is the notion of a field. This term may seem to be abstract, but it is indeed quite useful

For an event space $\mathcal{F}$ to be valid, $\mathcal{F}$ must be a [[Field]]. It is a field if it satisfies the following conditions:

- $\emptyset \in \mathcal{F}$ and $\Omega \in \mathcal{F}$.
- (Closed under complement) If $F \in \mathcal{F}$, then also $F^c \in \mathcal{F}$.
- (Closed under union and intersection) If $F_1 \in \mathcal{F}$ and $F_2 \in \mathcal{F}$, then $F_1 \cap F_2 \in \mathcal{F}$ and $F_1 \cup F_2 \in \mathcal{F}$.