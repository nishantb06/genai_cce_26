A **σ-algebra** (sigma-algebra) is a collection of subsets of some sample space Ω that is “closed under the operations probability theory needs.”

Think of it as: **which events are allowed to have a well-defined probability.**

---

### The three rules

A collection **F** of subsets of Ω is a σ-algebra if:

1. **Ω is in F** — “something happens” is an event.
2. **Closed under complements** — if A is an event, so is “not A”.
3. **Closed under countable unions** — if A₁, A₂, A₃, … are all events, then “A₁ or A₂ or A₃ or …” is also an event.

(From these, you also get countable intersections.)

---

### Why “sigma”?

**σ** means “countably many” (as in a countable sum/union). So a σ-algebra is an algebra of sets where you can combine events using complements and **countably infinite** unions — not just finitely many.

---

### Simple analogy

Imagine Ω = {1, 2, 3, 4, 5, 6} (a die).

- **Smallest σ-algebra:** {∅, Ω} — only “impossible” and “certain”.
- **A bigger one:** {∅, {2,4,6}, {1,3,5}, Ω} — you can talk about “even” vs “odd”.
- **Largest σ-algebra (power set):** every subset is an event.

For each choice, whenever you take complements or countable unions of allowed events, you stay inside the collection.

---

### Why it matters in probability

A [[Probability measure]] P assigns a number in [0, 1] to events. To do that consistently, you need a precise rule for which subsets count as events.

That rule is the σ-algebra **F**. Then (Ω, F, P) is a **probability space**:
- Ω = outcomes
- F = measurable events (σ-algebra)
- P = probabilities on those events

---

### Connection to [[Event space | Borel Sets]]

On the real line, you **cannot** sensibly assign probabilities to *every* subset of ℝ (Vitali-type sets break things).

So instead of “all subsets,” we use the **Borel σ-algebra**: the smallest σ-algebra containing all open intervals. That’s exactly what was meant by “the smallest σ-algebra containing every open set” in your note.

---

### One-line summary

> A **σ-algebra** is the set of events you’re allowed to measure — closed under “not” and “countably many ORs.”

If you want, I can also explain how this ties to your **Event space** note (power set vs Borel σ-algebra on ℝ) in that specific context.