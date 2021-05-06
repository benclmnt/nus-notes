## Chapter 2

- Lemma 2.3.2 (sometimes kita bs colok $\epsilon$ nya = 1 gitu...)
- Completeness Property of R (bounded above -> have sup)
- Bagi kasus $x > 1$ sama $x < 1$.
- Kalo mau prove $a = b$, kdg bisa use trichotomy property trus buktiin yg dua lainnya ga mgkn ato bs buktiin $a \leq b$ and $a \geq b$.
- Take median a.k.a. $\frac{a + b}{2}$.
- Kalo mau buktiin sup / inf, bs pake proof by contradiction, cari counter examplenya via density.
- Colok $\epsilon = awal - target$, supaya $awal - \epsilon$ -> $target$
- Abuse Archimedean property of $\mathbb{R}$ to find appropriate counter example.
- (hard) Construct a set, then abuse the definitions. :D

Sup -> exist infinitely many x s.t. x > Sup - epsilon!

## Chapter 3

Calculating Limits:

- Thm 3.2.11
- (Very Lose Stirling). $n! < n^n$.

Proving limits:
- If you know $(a_n) \rightarrow a$ (e.g. via Monotone Convergence Thm), then you can substitute $a_k$ with $a$ for any $k$ in the sequence definition to get the limit.
- If you want to prove a property regarding limits, try starting from the $\epsilon - K$ definition, then find appropriate (large enough) $n$
	- Construct $\epsilon$, to satisfy limit definition e.g. $\epsilon^2$, $\frac{\epsilon}{2}$, etc.
	- If $L < 1$, try $\epsilon = \frac{1 - L}{2} > 0$ -> we have $\frac{1 + L}{2} < 1$

More esoteric techniques.
- Try abuse expanding $(1 + x)^n > \frac{n(n-1)}{2}x^2$.
- (related to previous) Use $(1 + k_n)^n$ then prove that the sequence $(k_n)$ converges to 0.
- Calculating $\log y$ might be helpful.
- $b = \frac{1}{(1 + a)^n}$ for $0 < b < 1$ or $b = (1 + a)^n$ for $b > 1$ (?). Bernoulli ineq might be useful, or try binomial expansion.


Lim sup/lim inf
- To prove a property, just abuse definition
- To find limsup and liminf, 
    - first find the set of all possible values $V$ by partitioning $(x_n)$. 
    - To argue that $S(x_n)$ equals to all partition limits, use the following trick: Let $(x_{n_l})$ be a subsequence with limit $x \in S(x_n)$. $(x_{n_l})$ can be partitioned as well. Since $(x_{n_l})$ is an infinite sequence, one of the partitions, say $(x_{n_{l_m}})$ is infinite. By Thm 3.4.1, $\lim (x_{n_{l_m}}) = \lim (x_{n_l}) = x$. Since $(x_{n_{l_m}})$ is also a partition of $(x_n)$, then $x \in V$.
- Sometimes, you might want to abuse taking subsequence of subsequence and the fact that lim of subsequence = lim parent sequence.
- $\liminf x_n < c$ implies there is infinitely many $k$ s.t. $x_k < c$
- $\liminf x_n \leq \limsup x_n$.

Important Facts for proving convergence.
- Every convergent sequence is bounded. Every bounded and monotone sequence is convergent.
- Every bounded sequence has a convergent subsequence
- (trivial) Every subsequence of a bounded sequence is bounded.
- Every convergent sequence is Cauchy. Every Cauchy sequence is convergent (bounded).

Proving convergence of a sequence.
- If monotone and bounded, use monotone convergence theorem.
- If bounded, might be helpful to compare the sequence to other bounded sequence. (Thm 3.5.4)
- Check cauchy criterion
- If the sequence fluctuates (not monotone), check contractiveness and use Cauchy criterion. (Thm 3.6.4)

## Chapter 4

$\sum a_n$ converges ->(4.1.2) $(a_n)$ converges to 0 -> $(a_n)$ bounded.

Comparison Test vs Limit Comparison Test
- The CT and LCT are usually applied when the series resembles a geometric series or a p-series.
- Usually the LCT is simpler to apply than the CT.
- However, there are some cases where one has to use CT, e.g. when oscillating terms appear.

TO USE THE TEST: NEED TO PROVE THE PROPERTY OF EVENTUALLY NONNEG OR EVENTUALLY POS.

Proving convergence of a series:
1. Prove cauchy criterion either for sequence or series, because convergent iff cauchy.
2. n-th term test -> good to test divergence
3. Non-negative series: ratio test -> good for geometric series, series with n!, and certain series defined recursively, root test -> good for series where a_n involves nth power, CT or LCT -> good for comparing with geometric / p-series
4. Alternating series: alternating series test
5. Series with positive and negative terms: absolute and conditional convergence test

Convergence of series with square root -> try AM-GM?

## Chapter 6

c not an endpoint of I -> exist interval $(c - \mu, c + \mu) \in I$.

- To prove a function is not uniformly continuous, use seq criterion for uniform continuity.
- To prove a function is uniformly continuous, defive from definition
- To use uniformly continuous, if its a bounded interval, consider translating to continuous
- To use uniformly continuous
	- take $\delta > \frac{1}{M}$, and $y = x + \frac{1}{M}$ so that $| x - y | < \delta$.
	- take $\epsilon = 1$ (or some appropriate number).
	- Divide an unbounded interval into a bounded interval and the rest (unbounded interval). Prove uniform continuity in the unbounded interval, then combine the 2 interval. E.g. Tut 10 Q3.

## Chapter 7

- To prove open, use definition OR combine multiple open sets
- To prove closed set, either use characterization of closed set OR prove its complement is open.
- If $f$ is continuous, to prove open set -> Global Continuity Theorem
- To prove a set is not compact, show an open cover with no finite subcover.
