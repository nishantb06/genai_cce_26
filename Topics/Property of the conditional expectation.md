
Chain law and take the expectation on both sides  : Can it be proved like this ?

In reality we are manipulating  the [[Law of total expectations]] which is only for two random variables to multiple random variable 
We need to show that expectation of a function that depends on a and b wrt to the Conditional prob dist of a and b given c is a chain of two expectation as shown below
$$
\mathbb{E}_{A,B | C}[f(a,b)] = \mathbb{E}_{B | C}[\mathbb{E}_{A|B,C}[f(a,b)]]
$$

Writing LHS in terms of integrals
$$
\int\int f(a,b).p(a,b | c).da.db
$$
Using [[Chain rule of probability]]
$$
\int\int f(a,b).p(b | c).p(a | b,c).da.db
$$
Rearrange the integrals
$$
\int p(b|c) [{\int f(a,b) .p (a| b,c) da}] db
$$
Inner term is 
$$\mathbb{E}_{A|B,C}[f(a,b)]$$
and the outer term is another expectation
Thus LHS = RHS
