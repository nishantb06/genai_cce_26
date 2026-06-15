# Lebesgue Measure

## Example

$$A = [2, 3) \implies \mu(A) = 1$$
$$B = [3, 6] \implies \mu(B) = 3$$

For a set $[a, b] \subset \mathbb{R}$: $\mu([a,b]) = b - a$.

The Lebesgue measure is a mathematically precise notion of "length", "area", and "volume". It generalizes our intuitive idea of measuring sizes of sets.

Start with something familiar. On the real number line:

- The interval `[0, 1]` has length `1`.
- The interval `[2, 5]` has length `3`.
- The interval `(0, 2)` has length `2`.

The Lebesgue measure agrees with all of these intuitions.

For a set $A \subseteq \mathbb{R}$, its Lebesgue measure is usually denoted by $m(A)$ or $\lambda(A)$.

**Examples:**

- $m([0,1]) = 1$
- $m([2,5]) = 3$
- $m(\{1,2,3\}) = 0$ — a finite set of points has zero length
- $m(\mathbb{Q}) = 0$ — the rational numbers are countable, so they occupy no length despite being dense

This last example is one of the reasons Lebesgue measure is powerful. Between any two real numbers there are infinitely many rational numbers, yet their total "length" is zero.

## Why was it invented?

Classical notions of length work well for intervals but struggle for complicated sets.

For example, consider

$$A = [0,1] \setminus \mathbb{Q}$$

which is the set of irrational numbers in `[0,1]`.

Intuitively, removing the rationals should not change the length because rationals have measure zero. Lebesgue measure formalizes this:

$$m(A) = m([0,1]) - m(\mathbb{Q} \cap [0,1]) = 1 - 0 = 1$$

So almost all points in `[0,1]` are irrational.

## Properties

Lebesgue measure satisfies several natural properties.

### 1. Non-negativity

$$m(A) \ge 0$$

### 2. Empty set has measure zero

$$m(\emptyset) = 0$$

### 3. Length of intervals

$$m([a,b]) = b - a$$

### 4. Countable additivity

If $A_1, A_2, \dots$ are disjoint sets, then

$$m\left(\bigcup_{n=1}^{\infty} A_n\right) = \sum_{n=1}^{\infty} m(A_n)$$

For example,

$$m([0,1] \cup [2,3]) = 1 + 1 = 2$$

## How is it constructed?

The idea is:

1. Any set can be covered by intervals.
2. Add up the lengths of those intervals.
3. Among all possible coverings, take the smallest total length.

This gives the outer measure:

$$m^*(A) = \inf \left\{ \sum_{n=1}^{\infty}(b_n - a_n) : A \subseteq \bigcup_{n=1}^{\infty}(a_n, b_n) \right\}$$

Not every set behaves nicely with this definition. The sets for which this outer measure satisfies certain consistency conditions are called **Lebesgue measurable sets**, and the restriction of $m^*$ to these sets is the Lebesgue measure.

## Why does it matter?

Lebesgue measure is the foundation of the Lebesgue integral.

The ordinary integral computes areas by partitioning the x-axis into intervals. The Lebesgue integral instead groups together points where the function takes similar values and uses Lebesgue measure to determine how much of the domain contributes each value.

This makes it possible to integrate functions that are difficult or impossible to handle with the classical Riemann integral.

A useful intuition is:

- **Geometry:** Lebesgue measure answers *"How much space does this set occupy?"*
- **Integration:** Lebesgue integration answers *"How much of the domain has each function value?"*

You can think of Lebesgue measure as the rigorous mathematical notion of "size" on $\mathbb{R}^n$ that extends ordinary length, area, and volume to extremely complicated sets.
