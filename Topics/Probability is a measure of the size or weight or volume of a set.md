**Probability** is an operator that takes a set and tells us how large the set is.

The event "even number" on a die is a set containing $\{2, 4, 6\}$. When we apply probability to this set, we obtain $\frac{3}{6}$, as shown in Figure 2.1. Thus sets are the foundation of the study of probability.

Previous reading: [[Set Theory]]

Set theory tells us how to define the intersection so that the probability can be applied to the resulting set.

The term *size* makes sense when we are dealing with discrete events.

Let's now consider the term "size." Notice that the concept of the size of a set is not limited to the number of elements. A better way to think about size is to imagine that it is the weight of the set. This may seem fanciful at first, but it is quite natural. Consider the following example.

**Example 2.34.** (Continuous events with different weights) Suppose that the [[Sample space]] is an interval, say $\Omega = [-1, 1]$. On this interval we define a weighting function $f(x)$ where $f(x_0)$ specifies the weight for $x_0$. Because $\Omega$ is an interval, events defined on this $\Omega$ must also be intervals. For example, we can consider two events $E_1 = [a, b]$ and $E_2 = [c, d]$. The probabilities of these events are $P(E_1) = \int_a^b f(x)\, dx$ and $P(E_2) = \int_c^d f(x)\, dx$, as shown below.

![[Pasted image 20260706125340.png]]



Viewing probability as a measure is not just a game for mathematicians; rather, it has fundamental significance for several reasons. First, it eliminates any dependency on probability as relative frequency from the frequentist point of view. Relative frequency is a narrowly defined concept that is largely limited to discrete events, e.g., flipping a coin. While we can assign weights to coin-toss events to deal with those biased coins, the extension to continuous events becomes problematic. By thinking of probability as a measure, we can generalize the notion to apply to intervals, areas, volumes, and so on.

Second, viewing probability as a measure forces us to disentangle an event from measures. An event is a subset in the [[Sample space]]. It has nothing to do with the measure (e.g., a ruler) you use to measure the event. The measure, on the other hand, specifies the weighting function you apply to measure the event when computing the probability. For example, let $\Omega = [-1, 1]$ be an interval, and let $E = [a, b]$ be an event. We can define two weighting functions $f(x)$ and $g(x)$. Correspondingly, we will have two different [[Probability measure|probability measures]] $F$ and $G$ such that

$$
\begin{aligned}
F([a, b]) &= \int_E dF = \int_a^b f(x)\, dx, \\
G([a, b]) &= \int_E dG = \int_a^b g(x)\, dx.
\end{aligned}
$$

Now lets say the sample space is $\omega = [0,1]$ . Now what is the Probability measure of the event "**obtaining a single point**" {0.5} that is : $\mathbb{P}[\{0.5\}]$ . Even if we consider that we have a weighting function f(x) , f(0.5) will not be the answer we are seeking. 

The answer to this question is rooted in the **compatibility** between the measure and the sample space. In other words, the measure has to be meaningful for the events in the sample space. Using Ω=[0,1]Ω=[0,1], since Ω is an interval, an appropriate measure would be the length of this interval. You may add different weighting functions to define your measure, but ultimately, the measure must be an integral. If you use a “counter” as a measure, then the counter and the interval are not compatible because you cannot count on the real line. 

There are infinite elements in the set, so the probability of picking one point will tend to 0!

$$
\int_{0.5}^{0.5} f(x) dx = 0
$$
For any [[Probability Density | Weighting function]] the integral would be zero. 