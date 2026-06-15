Set of all subsets of $\Omega$ i.e the [[Sample space]]

## Borel sets

A **Borel set** is any subset of the real line (or $\mathbb{R}^n$) that you can build starting from open intervals using only:

- taking complements (everything *not* in the set), and
- taking countable unions or intersections (combining finitely or countably many sets at a time).

In practice: most "nice" subsets you care about in probability — intervals, single points, unions of intervals — are Borel sets. Pathological sets (like Vitali sets) are not.

Formally, the collection of all Borel sets is the smallest [[Sigma Algebra|σ-algebra]] containing every open set. When $\Omega = \mathbb{R}$, we often take the event space to be these Borel sets rather than *all* subsets of $\mathbb{R}$, because not every subset is measurable.
