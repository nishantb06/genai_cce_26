For a finite set, i.e., a set that contains $n$ elements, the collection of all possible subsets is indeed a field. This is not difficult to see if you consider rolling a die.

**Why bother constructing a field?**
The answer is that probability is a measure of the size of a set, so we must input a set to a [[Probability measure]] $P$ to get a number. The set being input to $P$ must be a subset inside the [[Sample space]] $\Omega$; otherwise, it will be undefined. If we regard $P$ as a mapping, we need to specify the collection of all its inputs, which is the set of all subsets, i.e., the [[Event space]] $\mathcal{F}$. So if we do not define the field, there is no way to define the measure $P$.

For countably infinite [[Sample space|sample spaces]], a plain [[Field]] is not enough — we need a [[Sigma Field|σ-field]] (equivalently, a [[Sigma Algebra|σ-algebra]]) that is closed under countable unions and intersections.
