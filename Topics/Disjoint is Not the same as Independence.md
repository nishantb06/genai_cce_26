If AA and BB are disjoint, then A∩B=∅A∩B=∅. This only implies that P[A∩B]=0P[A∩B]=0. However, it says nothing about whether P[A∩B]P[A∩B] can be factorized into P[A]P[B]P[A]P[B]. If AA and BB are independent, then we have P[A∩B]=P[A]P[B]P[A∩B]=P[A]P[B]. But this does not imply that P[A∩B]=0P[A∩B]=0. The only condition under which Disjoint ⇔⇔ Independence is when P[A]=0P[A]=0 or P[B]=0P[B]=0. Figure 2.30 depicts the situation. When two sets are independent, the conditional probability (which is a ratio) remains unchanged compared to unconditioned probability. When two sets are disjoint, they simply do not overlap.


Throw a die twice. Are AA and BB independent?A={1st die is 3}andB={sum is 7}.A={1st die is 3}andB={sum is 7}.

Solution

Note that

P[A∩B]=P[(3,4)]=136,P[A]=16,P[B]=P[(1,6),(2,5),(3,4),(4,3),(5,2),(6,1)]=16.P[A∩B]P[B]​=P[(3,4)]=361​,P[A]=61​,=P[(1,6),(2,5),(3,4),(4,3),(5,2),(6,1)]=61​.​

So P[A∩B]=P[A]P[B]P[A∩B]=P[A]P[B]. Thus, AA and BB are independent.

A pictorial illustration of this example is shown in Figure 2.32. Notice that whether the two events intersect is not how we determine independence (that only determines disjoint or not). The key is whether the conditional probability (which is the ratio) remains unchanged compared to the unconditioned probability.

![Figure 2.32](https://probability4datascience.com/eBook/pix/ch2_independence_example_02.png)

**Figure 2.32.** The two events AA and BB are independent because P[A]=16P[A]=61​ and P[A∩B]=136P[A∩B]=361​.

If we let B={sum is 8}B={sum is 8}, then the situation is different. The intersection A∩BA∩B has a probability 1551​ relative to BB, and therefore P[A∣B]=15P[A∣B]=51​. Hence, the two events AA and BB are dependent. If you like a more intuitive argument, you can imagine that BB has happened, i.e., the sum is 8. Then the probability for the first die to be 1 is 0 because there is no way to construct 8 when the first die is 1. As a result, we have eliminated one choice for the first die, leaving only five options. Therefore, since BB has influenced the probability of AA, they are dependent.