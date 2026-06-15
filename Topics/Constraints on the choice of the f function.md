Great question! Yes, there are precise constraints on what $f$ can be. Let's break them down:

## Required (Hard Constraints)

**1. Convexity — yes, mandatory** $f$ _must_ be convex. This is what guarantees $D_f \geq 0$ via **[[Jensen's inequality]]**:

$$D_f(P_X | P_\theta) = \mathbb{E}_{p_\theta}\left[f\left(\frac{p_X}{p_\theta}\right)\right] \geq f\left(\mathbb{E}_{p_\theta}\left[\frac{p_X}{p_\theta}\right]\right) = f(1) = 0$$

Without convexity, you lose the non-negativity guarantee — the "distance" could go negative, which is meaningless.

**2. $f(1) = 0$ — mandatory** This ensures $D_f(P | P) = 0$, i.e. a distribution has zero divergence from itself. Without this, you don't have a proper notion of "no difference."

**3. Domain $\mathbb{R}^+$ — mandatory** $f$ must be defined on positive reals since it takes the ratio $\frac{p_X(x)}{p_\theta(x)}$, which is always $> 0$.

**4. Left-semi-continuity — mandatory** This is a technical condition to handle cases where the supports of $P_X$ and $P_\theta$ don't fully overlap (i.e. the ratio $\frac{p_X}{p_\theta} \to \infty$ at the boundary). It ensures the integral is well-defined even in those edge cases.

---

## Not Required (Common Misconceptions)

**Symmetry — not required** $f(u)$ and $f(1/u)$ generate the same divergence only if $f$ is chosen specially. KL-divergence is the canonical example of an _asymmetric_ f-divergence.

**Boundedness — not required** KL-divergence is unbounded (it can go to $+\infty$ when supports don't overlap), yet it's perfectly valid. Total variation distance happens to be bounded in $[0,1]$, but that's a property of the specific $f$, not a requirement.

**Triangle inequality — not required** f-divergences are _not_ metrics in general. They don't need to satisfy the triangle inequality. Total variation distance is a special case that actually _does_ satisfy it, but most f-divergences (like KL) don't.

---

## Summary Table

|Property|Required?|Reason|
|---|---|---|
|$f$ convex|✅ Yes|Guarantees $D_f \geq 0$ via Jensen|
|$f(1) = 0$|✅ Yes|Zero divergence from self|
|Domain $\mathbb{R}^+$|✅ Yes|Ratio $p_X/p_\theta > 0$ always|
|Left-semi-continuous|✅ Yes|Well-definedness at boundary|
|Symmetric|❌ No|KL is asymmetric|
|Bounded|❌ No|KL is unbounded|
|Triangle inequality|❌ No|These are divergences, not metrics|
|Differentiable|❌ No|TV uses $|

The key intuition is: the constraints are the _minimum_ needed to make $D_f$ behave like a sensible "dissimilarity measure" — non-negative, and zero iff the distributions are identical. Everything beyond that is optional and gives different geometric/statistical properties.