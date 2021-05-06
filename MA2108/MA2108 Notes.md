# Real Analysis I (MA2108)
Bennett Clement

## Chapter 1

**Thm 1.1.1** $\sqrt{2}$ is an irrational number

**Thm 1.2.1 (Well-Ordering Property of $\mathbb{N}$)** Every nonempty subset $S$ of $\mathbb{N}$ has a least element, i.e. $\exists m \in S$ s.t. $m \leq n$ for all $n \in S$

**Thm 1.2.4 General mathematical Induction**:
Let $n_0 \in \mathbb{N}$. Suppose that 
1. $P(n_o)$ is true; and
2. for each natural number $k \geq n_0, P(k)$ is true $\longrightarrow P(k + 1)$ is true.

Then $P(n)$ is true for all natural numbers $n \geq n_0$.

**Thm 1.3.1 Algebraic properties of $\mathbb{R}$**
1. The binary operation **addition** satisfies Commutativity (A1), Associativity (A2), Existence of zero element (A3), Existence of inverse (A4)
2. The binary operation **multiplication** satisfies Commutativity (M1), Associativity (M2), Existence of zero element (M3), Existence of inverse (M4)
3. (D) Distributivity of multiplication over addition: $a \times (b + c) = a \times b + a \times c$.

Because of the properties (A1) - (A4), (M1) - (M4), and (D), we say that $(\mathbb{R}, + , \cdot)$ forms a **field**. 

Remark: $\mathbb{Q}$ forms a field, but $\mathbb{Z}$ and $\mathbb{N}$ do not.

**Thm 1.3.2**. Let $a, b, c \in \mathbb{R}$
1. *(Uniqueness of additive inverse)*. $a + b = 0 \rightarrow b = -a$
2. *(Uniqueness of multiplicative inverse)*. $((a \neq 0) \wedge (a \cdot b = 1)) \rightarrow b = \frac{1}{a}$
4. $a + b = b \rightarrow a = 0$
5. $(b \neq 0 \wedge a \cdot b = b ) \rightarrow a = 1$
6. $a \cdot 0 = 0$
7. $a \cdot b = 0 \rightarrow a = 0 \vee b = 0$
8. *(Cancellative property)* $(a \neq 0 \wedge (a \cdot b = a \cdot c)) \rightarrow b = c$

**Thm 1.3.3 (Order Properties of $\mathbb{R}$)**. Let $a,b,c,d \in \mathbb{R}$. A binary relation $>$ on $\mathbb{R}$ satisfies
1. (O1) $a > b \rightarrow a + c > b + c$
2. (O2) $((a > 0) \wedge (b > 0)) \rightarrow a \cdot b > 0$
3. (O3) (Trichotomy Property). Exactly one of the following holds: $a > b, \; a = b,  \; b > a$
4. (O4) (Transitive Property). $((a > b) \wedge (b > c)) \rightarrow a > c$

**Thm 1.3.4**. Let $a,b,c \in \mathbb{R}$, then:
1. $a > b \Leftrightarrow a - b > 0$. In particular $c < 0 \Leftrightarrow -c > 0$.
2. Exactly one of the following holds: $a > 0, \; a = 0,  \; b > 0$
3. If $a > b$ and $c > 0$, then $c \cdot a > c \cdot b$. If $a > b$ and $c < 0$, then $c \cdot a < c \cdot b$
4. If $a \geq b$ and $b \geq a$, then $a = b$

**Thm 1.3.6**. 
1. If $a \in \mathbb{R}$ and $a \neq 0$, then $a^2 > 0$
2. $1 > 0$
3. If $n \in \mathbb{N}$, then $n > 0$.
4. If $a > 0$, then $\frac{1}{a} > 0$

**Thm 1.3.7** If $a \in \mathbb{R}$ s.t. $0 \leq a < \epsilon$ for every positive number $\epsilon$, then $a = 0$.

Remark. If $a, b \in \mathbb{R}$ s.t. $a - \epsilon \leq b$ for every $\epsilon > 0$, then $a \leq b$.

**Bernoulli Ineq** If $x \geq -1$, then $(1 + x)^n \geq 1 + nx \quad \forall n \in \mathbb{N}$

Proof: Usual induction

**AM/GM/HM** Proof: Forward-backward induction.

**Thm 1.6.1** (Properties of absolute value). For all $a,b,c \in \mathbb{R}$
1. $\vert a \vert \geq 0$, $a \leq \vert a \vert$ and $-a \leq \vert a \vert$
2. $\vert a \vert = 0 \Longleftrightarrow a = 0$
3. $\vert - a \vert = \vert a \vert$
4. $\vert ab \vert = \vert a \vert \cdot \vert b \vert$
5. $\vert a \vert^2 = a ^2$
6. If $c \geq 0$, then $\vert a \vert \leq c \Longleftrightarrow -c \leq a \leq c$
7. $-\vert a \vert \leq a \leq \vert a \vert$

**Thm 1.6.2 (Triangle Ineq)**. $$\vert a \vert - \vert b \vert \leq \big\lvert \vert a \vert - \vert b \vert \big\rvert \leq \vert a \pm b \vert \leq \vert a \vert + \vert b \vert$$.

## 2 The Completeness of Real Numbers

### 2.1 Boundedness

Definition 2.1.1. A non-empty set of real numbers $S \subseteq \mathbb{R}$ is said to be **bounded above** if there exists some $M \in \mathbb{R}$ such that 
$$ x \leq M \quad \forall x \in S $$

Definition 2.1.3. A non-empty set is said to be **bounded** if it is bounded above and bounded below. 

Remarks: Upper bounds and lower bounds are not unique.

### 2.2 Maximum & Minimum

The **maximum** of a non-empty set of real numbers $S \subseteq \mathbb{R}$ is the **unique** upper bound $M$ that satisfies $M \in S$.

### 2.3 Supremum & Infimum

The **supremum** of a non-empty set of real numbers $S \subseteq \mathbb{R}$ is the **unique** i) upper bound $M$ that satisfies the property that ii) if $M'$ is an upper bound of $S$, then $M' \geq M$.

**Lemma 2.3.2.** $M = \sup S \Longleftrightarrow \forall \epsilon > 0, \exists x_\epsilon \in S$ s.t. $x_\epsilon > M - \epsilon$.

Remark: If $S$ has a maximum, then sup S = max S.

The **infimum** of a non-empty set of real numbers $S \subseteq \mathbb{R}$ is the **unique** i) lower bound $m$ that satisfies the property that ii) if $m'$ is an lower bound of $S$, then $m' \leq m$.

**Lemma 2.3.6.** $M = \inf S \Longleftrightarrow \forall \epsilon > 0, \exists x_\epsilon \in S$ s.t. $x_\epsilon < m + \epsilon$.

**2.3.7 Completeness Property of $\mathbb{R}$ **

Every **non-empty** subset of $\mathbb{R}$ which is **bounded above** (below) has a supremum (infimum) in $\mathbb{R}$.

### 2.4 Corollary of the completeness  property

**Thm 2.4.1 (Archimedean property of $\mathbb{R}$)** For any $x \in \mathbb{R}$, there exists $n_x \in \mathbb{N}$ s.t. $x < n_x$. 

Equivalently, we can say $\mathbb{N}$ is not bounded above in $\mathbb{R}$

**Corollary**: $\inf \left\{ \frac{1}{n} : n \in \mathbb{N} \right\} = 0$. In particular if $\epsilon > 0$, then there exists $n_\epsilon \in \mathbb{N}$ s.t. $0 < \frac{1}{n_\epsilon} < \epsilon$.

**Thm 2.4.5** (Existence of the positive k-th root of a positive real number). Let $c > 0, k \in \mathbb{N}$. Then there exists a unique, positive real number $a$ s.t. $a^k = c$.

**Thm 2.4.6 (Density Theorem)** For any $x, y \in \mathbb{R}$ s.t. $x < y$, there exists a rational number $q \in \mathbb{Q}$ s.t. $x < q < y$.

Proof: consequence of Archimedean property -> $\exists \, n$ s.t. $y - x > \frac{1}{n}$.

**Corollary**: Let $\alpha \in \mathbb{R}$ and $E = \{ x \in \mathbb{Q} : x < \alpha \} \subseteq \mathbb{Q}$, then sup $E = \alpha$.

Def 2.4.9. A subset D of $\mathbb{R}$ is said to be **dense** in $\mathbb{R}$ if for any $a, b \in \mathbb{R}$ with $a < b$, $D \cap (a, b) \neq \emptyset$

**Fact**: $\mathbb{R} \setminus \mathbb{Q}$ and $\mathbb{Q}$ are dense in $\mathbb{R}$.

### 2.5 More on Intervals

Definition. An interval is a subset $I$ of $\mathbb{R}$ s.t. if $x < t < y$ and $x, y \in I$, then $t \in I$.

## 3 Sequences

### 3.1 Preliminary definitions

Definition. a **sequence** in $\mathbb{R}$ is a real-valued function $X : \mathbb{N} \rightarrow \mathbb{R}$.

Definition. Let $a \in \mathbb{R}$ and $\epsilon > 0$. The $\epsilon$-neighborhood of $a$ is the set $(a - \epsilon, a + \epsilon)$.

$(\epsilon -K)$ Definition. $x$ is the **limit** of $(x_n)$ (or $(x_n)$ converges to $x$) if for every $\epsilon > 0$, there exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $| x_n - x | < \epsilon$ for all $n \geq K$.

**Thm 3.1.1** If $(x_n)$ converges, then it has exactly one limit.

### 3.2 Limit Theorems

**NOTE**: Unless specified otherwise, all limits in this section are defined for $n \rightarrow \infty$.

Definition. A sequence $(x_n)$ is said to be **bounded** if there exists $M > 0$ s.t. $| x_n| \leq M$ for all $n \in \mathbb{N}$.

**Thm 3.2.1** Every convergent sequence is bounded.

The reverse (see Thm 3.3.1).

**Thm 3.2.3 (Squeeze Thm)** If $x_n \leq y_n \leq z_n$ for all $n \geq K_0$ and $\lim x_n = \lim z_n = a$, then $\lim y_n = a$.

**Thm 3.2.4**. If $\vert x_n \vert \rightarrow 0$, then $x_n \rightarrow 0$.

**3.2.11** List of limits of some standard sequences.
- For a fixed number $\vert b \vert < 1$, we have $\lim b^n = 0$.
- For a fixed number $c > 0$, we have $\lim c^\frac{1}{n} = 1$.
- $\lim n^\frac{1}{n} = 1$
- $\lim \left(1 + \frac{1}{n} \right)^n = e$ -> proven in Ex 3.3.5
- $n^k << n^l << a^n << b^n << n!$ if $k < l$ and $1 < a < b$.
- If $(x_n)$ and $(y_n)$ converges, taking the operations $+, -, \times, \div$ (only if $y_n \neq 0$ and $\lim y_n \neq 0$), $\vert \; \vert, \sqrt{\;}$ and the inequality signs $\leq$ and $\geq$ under limit preserves the convergence.

### 3.3 Monotone Sequences

Definition. We say that the sequence $(x_n)$ is
1. increasing if $x_1 \leq x_2 \leq \cdots \leq x_n \leq \cdots$
2. decreasing if $x_1 \geq x_2 \geq \cdots \geq x_n \geq \cdots$
3. monotone if it is either increasing or decreasing.

**Thm 3.3.1 (Monotone Convergence Theorem)** If $(x_n)$ is monotone and bounded, then $(x_n)$ converges. In particular $\lim x_n$ equals to $\sup \{x_n : n \in \mathbb{N}\}$ if $(x_n)$ is increasing, or $\inf \{x_n : n \in \mathbb{N}\}$ if $(x_n)$ is decreasing.

### 3.4 Subsequences

Definition. Let $(x_n)$ be a sequence and let $n_1 < n_2 < \cdots < n_k < \cdots$ be a strictly increasing sequence of natural numbers. Then the sequence $(x_{n_k})$ is called a **subsequence** of $(x_n)$

Remark: If $(y_k) = (x_{n_k})$ is a subsequence of $(x_n)$, then $n_k \geq k$.

**Thm 3.4.1**. If $(x_n)$ converges to $x$, then any subsequence $(x_{n_k})$ also converges to $x$.

Corollary 3.4.2. If $(x_n)$ has a divergent subsequence, then $(x_n)$ diverges.
Corollary 3.4.3. If $(x_n)$ has two convergent subsequences whose limits are not equal, then $(x_n)$ diverges.

**Thm 3.4.4 (Monotone Subsequence Theorem)** Every sequence has a monotone subsequence

**Thm 3.4.5 (Bolzano-Weierstrass Theorem)** Every bounded sequence has a convergent subsequence.

### 3.5 Lim sup and lim inf

Definition. Let $(x_n)$ be a sequence. $x \in \mathbb{R}$ is called the **subsequential limit** of $(x_n)$ if $(x_n)$ has a subsequence which converges to $x$. 

Definition. Let $S(x_n)$ be the set of all subsequential limits of $(x_n)$. 

Definition. Let $(x_n)$ be a **bounded** sequence. We know from Bolzano-Weierstrass Theorem, that $S(x_n)$ is non-empty and from Thm 3.2.11 that $S(x_n)$ is bounded.
1. $\limsup x_n := \sup S(x_n)$
2. $\liminf x_n := \inf S(x_n)$.

**Thm 3.5.1** Let $(x_n)$ be a bounded sequence and let $M = \limsup x_n$.
1. $\forall \epsilon > 0$, there are at most finitely many $n$'s such that $x_n \geq M + \epsilon$. Equivalently, $\forall \epsilon > 0$, exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $x_n < M + \epsilon$ for all $n \geq K$.
2.  $\forall \epsilon > 0$, there are infinitely many $n$'s such that $x_n > M - \epsilon$. Equivalently, $\forall \epsilon > 0$ exists a subsequence $(x_{n_k})$ of $(x_n)$ s.t. $x_{n_k} > M - \epsilon$ for all $k \in \mathbb{N}$.

**Thm 3.5.2** Let $(x_n)$ be a bounded sequence and let $m = \liminf x_n$.
1. $\forall \epsilon > 0$, there are at most finitely many $n$'s such that $x_n \leq m - \epsilon$. Equivalently, $\forall \epsilon > 0$, exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $x_n > m - \epsilon$ for all $n \geq K$.
2.  $\forall \epsilon > 0$, there are infinitely many $n$'s such that $x_n < m + \epsilon$. Equivalently, $\forall \epsilon > 0$ exists a subsequence $(x_{n_k})$ of $(x_n)$ s.t. $x_{n_k} < m + \epsilon$ for all $k \in \mathbb{N}$.

**Thm 3.5.3** Let $(x_n)$ be a bounded sequence. Then $(x_n)$ converges (to $x$) iff $\limsup x_n = \liminf x_n = x$.

**Thm 3.5.4**. Let $(x_n)$ and $(y_n)$ be bounded sequences s.t. $x_n \leq y_n$ for all $n$. Then $\limsup x_n \leq \limsup y_n$ and $\liminf x_n \leq \liminf y_n$.

Thm 3.5.5 (Alternative definition of lim sup). Let $(x_n)$ be a bounded sequence. Let $y_n = \sup \{ x_k : k \geq n \} \;, \; \forall n \in \mathbb{N}$. Then the sequence $(y_n)$ is decreasing and bounded, and $\limsup x_n = \lim y_n$.

### 3.6 Cauchy Criterion

Definition. A sequence $(x_n)$ is called a **Cauchy sequence** if for every $\epsilon > 0$, there exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $\vert x_n - x_m \vert < \epsilon$ for all $n > m \geq K$.

**Thm 3.6.1** Every convergent sequence is Cauchy.

**Thm 3.6.2** Every Cauchy sequence is bounded.

**Thm 3.6.3 (Cauchy Criterion)** Every Cauchy sequence is convergent.

A sequence $(x_n)$ is called a contractive sequence if there exists some constant $0 < C < 1$, s.t. $\vert x_{n + 2} - x_{n + 1} \vert \leq C \vert x_{n + 1} - x_n \vert$ for all $n \in \mathbb{N}$.

**Thm 3.6.4** Every contractive sequence is Cauchy. 

### 3.7 Properly divergent sequences

($M - K$) Definition. We say that a sequence $(x_n)$ tends to $\infty$ if for every $M > 0$, there exists $K = K(M) \in \mathbb{N}$ s.t. $x_n > M$ for all $n \geq K$. 

Similar definition (change signs) for tending to $- \infty$.

**Thm 3.7.1** If a sequence $(x_n)$ is increasing and not bounded above, then $x_n \rightarrow \infty$.

Definition. We call a sequence $(x_n)$ **properly divergent** if either $x_n \rightarrow \infty$ or $x_n \rightarrow -\infty$.

(Bartle, Thm 3.6.3) A monotone sequence of real numbers is properly divergent iff it is unbounded.

(Bartle, Thm 3.6.4) Let $(x_n)$ and $(y_n)$ be 2 sequences of real numbers s.t. $x_n \leq y_n$ for all $n \in \mathbb{N}$. Then if $\lim x_n = +\infty$, then $\lim y_n = +\infty$. If $\lim y_n  = -\infty$, then $\lim x_n = -\infty$.

(Bartle, Thm 3.6.5) Let $(x_n)$ and $(y_n)$ be 2 sequences of real numbers s.t. $\lim \frac{x_n}{y_n} = L$ for some $L \in \mathbb{R}, L > 0$. We have $\lim x_n = +\infty$ iff $\lim y_n = +\infty$.

#### Comparison of properly divergent sequences

Let $(x_n)$ and $(y_n)$ be two sequences of positive numbers s.t. $\lim x_n = \infty$ and $\lim y_n = \infty$. We write $x_n = o(y_n)$ or $x_n << y_n$ if $\lim \frac{x_n}{y_n} = 0$. 

Remark 3.7.6. the above relation $<<$ is transitive.
Remark 3.7.7. $n^k << n^l << a^n << b^n << n!$ if $k < l$ and $1 < a < b$.

**Indeterminate forms**: $\frac{\infty}{\infty}, \frac{0}{0}, 0 \cdot \infty, \infty - \infty, 0^0, 1^\infty, \infty^0$.

#### Tutorial results
- (Tut 3 Q2) If $(a_n)$ converges and $\vert a_n + nb_n \vert < 1$ for all $n \in \mathbb{N}$, then the sequence $(b_n)$ converges.
- (Tut 3 Q4) If $(x_n)$ is convergent and $(y_n)$ is divergent, then $(x_n + y_n)$ is divergent.
- (Tut 3 Q4) If $(x_n)$ is divergent and $(y_n)$ is convergent (not to 0), then $(x_ny_n)$ is divergent. 
- (Tut 3 Q5) If $(x_n) \rightarrow x$, then AM, GM, HM converges to $x$.
- Example 3.3.5. $(e_n) = \left( 1 + \frac{1}{n}\right)^n$ is increasing and bounded.
- (Tut 3 Q6. Similar to Ratio Test). Let $(x_n)$ be a sequence of **positive** real numbers such that $L := \lim \frac{x_{n+1}}{x_n}$ exists. If $L < 1$, then $(x_n)$ converges and $\lim x_n = 0$.
- (Tut 4 Q5) $\limsup (x_n + y_n) \leq \limsup x_n + \limsup y_n$. Similarly $\liminf (x_n + y_n) \geq \liminf x_n + \liminf y_n$
- (Tut 5 Q3) If $x_n > 0$ for all $n$, then $\lim x_n = 0$ iff $\lim \frac{1}{x_n} = \infty$.
- (Tut 5 Q4) Let $(x_n)$ and $(y_n)$ be sequence of *positive* numbers s.t. $\lim\frac{x_n}{y_n} = \infty$.
	- If $y_n \rightarrow \infty$, then $x_n \rightarrow \infty$.
	- If $(x_n)$ is bounded, $y_n \rightarrow 0$.

## 4 Infinite Series

Notation: For the following chapter, $\sum$ is equivalent $\sum\limits_{n=1}^{\infty}$ otherwise stated.

### 4.1 Definition and Examples

Definition 4.1.1. Given a series $\sum a_k$, define its $n$-th **partial sum**  as $s_n = \sum a_k = a_1 + a_2 + \cdots + a_n$.

The sequence $(s_n)$ is called the **sequence of partial sums** of the series $\sum a_k$.

Definition 4.1.2. Consider the sequence of partial sums $(s_n)$ of the series $\sum a_k$. We say that the series **converges** (to $S$) and write $\sum a_k = \lim s_n = S$ if and only if $(s_n)$ converges to a number $S \in \mathbb{R}$.

**Remark 4.1.1. (Geometric Series)**. $\sum\limits_{k=1}^\infty ar^{k-1}$ converges to $\frac{a}{1-r}$ if $\vert r \vert < 1$ and diverges otherwise.

**Thm 4.1.1** Let $\sum a_k$ and $\sum b_k$ be two convergent series and let $c \in \mathbb{R}$.
1. The series $\sum(a_k + b_k)$ is convergent and equals $\sum a_k$ + $\sum b_k$
2. The series $\sum ca_k$ is convergent and equals $c\sum a_k$

**Thm 4.1.2** If $\sum a_n$ converges, then $\lim a_n = 0$. 

**Thm 4.1.3 (The n-th term divergence test)**.
1. If $\lim a_n \neq 0$ or do not exists, then $\sum a_n$ diverges.
2. If $\lim a_n = 0$, we can conclude NOTHING about the series $\sum a_n$

**Thm 4.1.4 (Cauchy criterion for series)**. The series $\sum a_n$ converges iff for all $\epsilon > 0$, there exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $\vert a_{n + 1} + a_{n + 2} + \cdots a_m \vert < \epsilon$ for all $m > n \geq K$.

### 4.2 Series with nonnegative terms

Goal: Given a series, test whether the series converges.

Definition 4.2.1. A series $\sum a_k$ is called an **eventually non-negative  (positive) series** there exists $K \in \mathbb{N}$ s.t. $a_k \geq 0$ ($a_k > 0$) for all $k \geq K$.

**Thm 4.2.1** Let $\sum a_n$ be an eventually non-negative series. Then $\sum a_n$ converges iff the sequence $(s_n)$ of partial sums is bounded above.

**Remark 4.2.4 (p-series)** If $p > 1$, then the $p$-**series** $\large \sum \frac{1}{n^p}$ converges. If $p \leq 1$, then the $p$-series diverges.

**Thm 4.2.3 (Comparison Test)** Consider 2 **eventually non-negative** series $\sum a_k$ and $\sum b_k$. Suppose there exists $K \in \mathbb{N}$ s.t. $0 \leq a_k \leq b_k$ for all $k \geq K$. If $\sum b_k$ converges, then $\sum a_k$ converges.

Remark 4.2.5. When applying comparison test, we try to compare a given series with either a **bigger but convergent** series or a **smaller but divergent** series. The two standard series often used in comparison tests are the p-series and the geometric series $\sum ar^{n-1}$ 

**Thm 4.2.5 (Limit Comparison Test)** Let 2 **eventually positive** series $\sum a_n$ and $\sum b_n$ and suppose that the limit $\rho = lim \frac{a_n}{b_n}$ exists.
1. If $\rho > 0$, then either both converge or both diverge
2. If $\rho = 0$ and $\sum b_n$ converges, then $\sum a_n$ converges.

Intuition: 
1. The two series resemble finite non-zero multiple of each other
2. $\sum a_n$ is smaller than $\sum b_n$ -> similar to comparison test.

**Thm 4.2.7 (Ratio Test)**. Let $\sum a_n$ be an **eventually positive** series. and suppose that the limit $\large \rho = \lim \frac{a_{n + 1}}{a_n}$ exists. 
- If $\rho < 1$, the series converges. --> Note: can use $\limsup$ as well.
- If $\rho > 1$, the series diverges.
- No conclusion if $\rho = 1$.

**Thm 4.2.8 (Root Test)**. Let $\sum a_n$ be an **eventually non-negative** series. and suppose that the $(a_n^{1/n})$ is a bounded sequence. Let $\rho = \limsup a_n^{1/n}$. 
- If $\rho < 1$, the series converges.
- If $\rho > 1$, the series diverges.
- No conclusion if $\rho = 1$.

### 4.3 Alternating Series
Definition 4.3.1. An alternating series is a series of the form $\sum(-1)^{k + 1}a_k$ or $\sum(-1)^ka_k$

**Theorem 4.3.1 (Alternating Series Test)** Let $\sum(-1)^ka_k$ be an alternating series. Suppose that $a_n \geq 0$ for all $n$, $(a_n)$ is decreasing, and $\lim a_n = 0$. Then the series is convergent.

### 4.4 Absolute and Conditional convergence

For series with both +-ve and -ve terms.

Definition 4.4.1. 
1. We say that the series $\sum a_n$ **converges absolutely** if the series $\sum \vert a_n \vert$ converges.
2. We say that the series $\sum a_n$ **converges conditionally** if $\sum a_n$ converges but $\sum \vert a_n \vert$ diverges.

**Theorem 4.4.1** If the series $\sum a_n$ converges absolutely, then it converges.

**Theorem 4.4.2** Every series is either absolutely convergent, conditionally convergent or divergent.

### Dirichlet and Abel Tests

**Abel's Lemma**. Let $X := (x_n)$ and $Y := (y_n)$ be sequences in $\mathbb{R}$ and let the partial sums of $\sum  y_n$ be denoted by $(s_n)$ with $s_0 = 0$. If $m > n$, then $\sum\limits_{k=n + 1}^m x_ky_k = (x_ms_m - x_{n+1}s_n) + \sum\limits_{k = n + 1}^{m - 1}(x_k - x_{k + 1}) s_k$

**Dirichlet's Test**. If $(x_n)$ is a decreasing sequence with $\lim x_n = 0$ and if the partial sums $(s_n)$  of $\sum y_n$ are bounded, then the series $\sum x_ny_n$ is convergent.

**Abel's Test**. If $(x_n)$ is a convergent monotone sequence and the series $\sum y_n$ is convergent, then the series $\sum x_ny_n$ is also convergent.

#### Tutorial Results

- (Tut 6 Q2). If $\sum a_n$ is convergent, the series of its AM is divergent.

## 5 Limits of Functions

Definition 5.2.1 Let $\emptyset \neq A \subseteq \mathbb{R}$. A real number $c$ is a **cluster point** of $A$ if for every $\delta > 0$, there exists a point $x \in A \backslash \{c\}$ s.t. $0  < \vert x - c \vert < \delta$.

Remark. A cluster point $c$ of a set $A$ need not be an element of $A$.

Proposition 5.2.1. A real number $c$ is a cluster point of $\emptyset \neq A \subseteq \mathbb{R}$ if and only if there exists a sequence $(a_n)$ in $A \backslash \{c\}$ s.t. $\lim a_n = c$.

**Definition 5.2.2. ($\epsilon - \delta$ definition of limit).** Let $f : A \rightarrow \mathbb{R}$ be a function, where $\emptyset \neq A \subseteq \mathbb{R}$ and let $c$ be a cluster point of $A$. We say that $\lim\limits_{x \rightarrow c} f(x) = L$ if for every $\epsilon > 0$, there exists $\delta = \delta(\epsilon) > 0$ s.t. $\vert f(x) - L \vert < \epsilon$ for all $x \in A$ satisfying $0 < \vert x - c \vert < \delta$.

If the limit of $f$ at $x = c$ does not exist (in $\mathbb{R}$), we say that $f$ **diverges** at $x = c$.

Definition: 
- If $h > 0$, then the **$h$-neighborhood** of the point $a$ is the set $V_h(a) = \{ x : \vert x - a \vert < h \} = (a - h , a + h)$.
- Define $V_h^*(a) = V_h(a) \backslash \{a\} = \{ x : 0 < \vert x - a \vert < h \}$ as the **deleted neighborhood** of $a$.

Remark: 
1. If $c$ is not a cluster point of $A$, then there exists $\delta > 0$ s.t. $A \cap V_\delta^*(c) = \emptyset$.
2. We can rewrite definition 5.2.2 as $\lim\limits_{x \rightarrow c} f(x) = L$ iff for any given $\epsilon > 0$, there exists $\delta = \delta(\epsilon) > 0$ s.t. $f(A \cap V_\delta^*(c)) \subseteq V_\epsilon(L)$.
3. The limit of a function at a cluster point is unique if the limit exists.

**Theorem 5.2.3. (Sequential Criterion for Limits)**. Let $\emptyset \neq A \subseteq \mathbb{R}$ and let $c$ be a cluster point of $A$. Suppose that $f : A \rightarrow \mathbb{R}$ and $L \in \mathbb{R}$. Then the following statements are equivalent: ^1a90f2
1. $\lim\limits_{x \rightarrow c} f(x) = L$
2. For every sequence $(x_n)$ in $A \backslash \{c\}$ s.t. $\lim x_n = c$, one has $\lim f(x_n) = L$

**Theorem 5.2.4 (Uniqueness of limits)**
If $f : A \rightarrow \mathbb{R}$ is a function and $c$ is a cluster point of $A$, the the limit of $f$ at $x = c$ is unique if it exists.

Remark 5.2.6 (Divergence Criteria). Let $f : A \rightarrow \mathbb{R}$ be a function and let $c$ be a cluster point of $A$. To prove $\lim\limits_{x \rightarrow c} f(x)$ does not exist ,either:
1. Find a sequence $(x_n)$ in $A \backslash \{c\}$ s.t. $\lim x_n = c$, but the sequence $(f(x_n))$ diverges.
2. Find 2 sequences $(x_n)$ and $(y_n)$ in $A \backslash \{c\}$ s.t.  $\lim x_n = c = \lim y_n$ but $\lim f(x_n) \neq \lim f(y_n)$. 

### 5.3 Limit Theorems

Assume $f : A \rightarrow \mathbb{R}$ is a function and $c$ is a cluster point of $A$.

**Theorem 5.3.1** If $\lim\limits_{x \rightarrow c} f(x)$ exists, then there exist constants $M, \delta > 0$ s.t. $\vert f(x) \vert \leq M$ for all $x \in A$ satisfying $0 < \vert x - c \vert < \delta$.

**Basic Principle 5.3.5** Suppose there exists a deleted neighborhood $V_h^*(c)$ (with $h > 0$) s.t. $f(x) = g(x)$ for all $x \in A \cap V_h^*(c)$, then $\lim\limits_{x \rightarrow c} f(x) = \lim\limits_{x \rightarrow c} g(x)$ provided one of these limits exist.

If $\lim\limits_{x \rightarrow c} f(x)$ and $\lim\limits_{x \rightarrow c} g(x)$ exists, applying the operations $+, -, \times, \div$ (only if $g(x) \neq 0$ for all $x \in A$), $\vert \; \vert, \sqrt{\;}$ and the inequality signs $\leq$ and $\geq$ between the functions is the same as applying it to their limits.

**Theorem 5.3.7. (Squeeze Theorem)** Let $f,g,h$ be three functions and let $c$ be a cluster point of $A$. Suppose that $f(x) \leq g(x) \leq h(x)$ for all $x \in A$ satisfying $0 < \vert x - c \vert < \delta$ and $\lim\limits_{x \rightarrow c} f(x) = \lim\limits_{x \rightarrow c} h(x) = L$, then $\lim\limits_{x \rightarrow c} g(x) = L$.

**Theorem 5.3.8** If $\lim\limits_{x \rightarrow c} f(x) = L$ exists and $L > 0$, then exists $\delta > 0$ s.t. $f(x) > 0$ for all $x \in A$ satisfying $0 < \vert x - c \vert < \delta$.

### 5.4 One sided limits

Definition 5.4.1.  
1. Let $c$ be a cluster point of $A \cap (c, \infty)$. We say that $L$ is the **right-hand limit** of $f$ at $c$, denoted by $\lim\limits_{x \rightarrow c^+} f(x)$,  if for any given $\epsilon > 0$, there exists $\delta = \delta(\epsilon) > 0$ s.t. $\vert f(x) - L \vert < \epsilon$ for all $x \in A$ satisfying $c < x < c + \delta$.
2. Let $c$ be a cluster point of $A \cap (-\infty, c)$. We say that $L$ is the **left-hand limit** of $f$ at $c$, denoted by $\lim\limits_{x \rightarrow c^-} f(x)$, if for any given $\epsilon > 0$, there exists $\delta = \delta(\epsilon) > 0$ s.t. $\vert f(x) - L \vert < \epsilon$ for all $x \in A$ satisfying $c - \delta < x < c$. 

**Theorem 5.4.2** $\lim\limits_{x \rightarrow c} f(x) = L$ iff both left-hand limit and right-hand limit exists and is equal to $L$.

**Theorem 5.4.4. (Sequential Criterion for right-hand Limits)**.Suppose that $f : A \rightarrow \mathbb{R}$ and let $c$ be a cluster point of $A \cap (c, \infty)$. Then the following statements are equivalent:
1. $\lim\limits_{x \rightarrow c^+} f(x) = L$
2. For every sequence $(x_n)$ in $A \cap (c, \infty)$ s.t. $\lim x_n = c$, one has $\lim f(x_n) = L$

There is a similar sequential criterion for the left-hand limit.

**Note:** All limit theorems (squeeze, operations, basic principle 5.3.5) also holds for one-sided limits.

### 5.5 Infinite Limits

Definition: We say that $\lim\limits_{x \rightarrow c} f(x) = + \infty$ if for every $M > 0$, there exists $\delta = \delta(M) > 0$ s.t  $f(x) > M$ for all $x \in A$ satisfying $0 < \vert x - c \vert < \delta$. 

We have a similar definition for tending to $-\infty$.

**Note**
- There is a similar sequential criterion for the infinite limits, ([[MA2108 Notes#^1a90f2 | Theorem 5.2.3]]), and infinite one-sided limits (Theorem 5.4.4) with $L = \infty$
- We have a stronger statement than Squeeze Theorem, i.e. if $f(x) \geq g(x)$ for all $x$ in domain and $\lim g(x) = \infty$, then $\lim f(x) = \infty$.

### 5.6 Limits at infinity

Definition 5.6.1.
1. Suppose $A$ is not bounded above. We say that $\lim\limits_{x \rightarrow \infty} f(x) = L$ if for every $\epsilon > 0$, there exists $M = M(\epsilon) > 0$ s.t. $\vert f(x) - L \vert < \epsilon$ for all $x \in A$ and $x > M$.
2. Suppose $A$ is not bounded below. We say that $\lim\limits_{x \rightarrow -\infty} f(x) = L$ if for every $\epsilon > 0$, there exists $M = M(\epsilon) < 0$ s.t. $\vert f(x) - L \vert < \epsilon$ for all $x \in A$ and $x < M$.

Remark 5.6.2. The concept of the limit of a sequence is a special case of the above definition (with $A = \mathbb{N}$).

**Theorem 5.6.3 (Sequential Criterion for limit at infinity)** Suppose that $f : A \rightarrow \mathbb{R}$ and suppose $A$ is not bounded above. Then the following statements are equivalent:
1. $\lim\limits_{x \rightarrow \infty} f(x) = L$
2. For every sequence $(x_n)$ in $A$ s.t. $\lim x_n = \infty$, one has $\lim f(x_n) = L$

**Note:** All limit theorems (squeeze, operations, basic principle 5.3.5) also holds for limits at infinity.

### 5.7 Infinite limits at infinity

Definition 5.7.1. Suppose $A$ is not bounded above. We say that $\lim\limits_{x \rightarrow \infty} f(x) = \infty$ if for every $M > 0$, there exists $K = K(M) > 0$ s.t. $f(x) > M$ for all $x \in A$ and $x > K$.

**Note**
- There is a similar sequential criterion (Theorem 5.6.3 with $L = \infty$)

### Tutorial Results

- (Tut 8 Q3) Suppose $\lim\limits_{x \rightarrow a} f(x) = L > 0$ and $\lim\limits_{x \rightarrow a} g(x) = \infty$, then $\lim\limits_{x \rightarrow a} f(x)g(x) = \infty$.

## 6 Continuous Functions

**Definition 6.1.1. ($\epsilon - \delta$ definition of continuity).** A function $f : A \rightarrow \mathbb{R}$ is said to be **continuous at** $x = a \in A$  if for every $\epsilon > 0$, there exists $\delta = \delta(\epsilon, a) > 0$ s.t. $\vert f(x) - f(a) \vert < \epsilon$ for all $x \in A$ satisfying $\vert x - a \vert < \delta$.

- If $f$ is not continuous at $a$, we say that $f$ is **discontinuous** at $x = a$ and $a$ is a **point of discontinuity** of $f$.
- If $f$ is continuous at every point in $A$, we say that $f$ is continuous on $A$.
- If $a \in A$ is not a cluster point of $A$, then $f$ is always continuous at $a$ since there exists $\delta > 0$ s.t. $A \cap (a - \delta, a + \delta) = \{ a \}$
- If the choice of $\delta$ only depends on $\epsilon$, the function is said to be [[MA2108 Notes#6 5 Uniform continuity|uniformly continuous]] 

**Theorem 6.1.1 (Continuity in terms of limits)**. If $a \in A$ is a cluster point of $A$, then $f$ is continuous at $x = a$ iff $\lim\limits_{x \rightarrow a} f(x) = f(a)$.

**Theorem 6.1.6. (Sequential Criterion for Continuity)**. We have something similar to Theorem 5.2.3 (Sequential criterion for limits) with $L = f(a)$ and domain of $(x_n)$ is $A$.

Summary of common continuous functions
1. Polynomials, absolute-value functions, sine and cosine functions are continuous on $\mathbb{R}$.
2. nth-root functions are continuous on $(0, \infty)$.
3. Rational functions $p(x) / q(x)$ are continuous everywhere except at the zeros of $q$.
4. Floor function is continuous on $\mathbb{R} \backslash \mathbb{Z}$ (and is discontinuous at each $a \in \mathbb{Z}$)

**Remark**: Sometimes we can "save" a function which is discontinuous at a point, i.e. if $\lim\limits_{x \rightarrow a}f(x) = L$ exists but $f(a)$ is not defined, then we can simply define $f(a) = L$ and the resulting function will now be continuous at $a$.

### 6.2 Combinations of continuous functions

**Theorem 6.2.1**. Let $A \subseteq \mathbb{R}$ and let $f, g : A \rightarrow \mathbb{R}$ be continuous functions at $a \in A$. Let $k \in \mathbb{R}$. Then the functions $f + g, f - g, kf$ and $f \cdot g$ are all continuous at $x = a$. If $g(a) \neq 0$, then the function $f / g$ is also continuous at $x = a$.

**Theorem 6.2.2.** Composition of continuous functions is continuous provided the image of the inner functions fall inside the domain of the outer function.

### 6.3 Continuous functions on intervals

Definition 6.3.1. A function $f: A \rightarrow \mathbb{R}$ is said to be **bounded on A** if the image $f(A)$ is a bounded set.

**Theorem 6.3.1.** Let $f : [a,b] \rightarrow \mathbb{R}$ be a continuous function on the **closed bounded** interval $[a, b]$. Then $f$ is bounded on $[a, b]$.

Definition 6.3.2. We say that $f$ has an **absolute maximum** on $A$, denoted $\max f(A)$, if there exists $y \in A$ s.t. $f(y) \geq f(x)$ for all $x \in A$.

**Theorem 6.3.3. (Extreme Value Theorem)** Suppose that $f : [a,b] \rightarrow \mathbb{R}$ is a continuous function on the closed bounded interval $[a, b]$. Then $f$ has an absolute maximum and an absolute minimum on $[a, b]$.

**Theorem 6.3.5. (Intermediate Value Theorem)** Suppose that $f : [a,b] \rightarrow \mathbb{R}$ is a continuous function on the closed bounded interval $[a, b]$. Then for any number $L$ strictly between $f(a)$ and $f(b)$, there exists $c \in (a,b)$ s.t. $f(c) = L$.

Corollary: We have $[f(a), f(b)] \subseteq f([a, b])$

**Theorem 6.3.7.** A continuous function sends a closed bounded interval onto a closed bounded interval.

**Theorem 6.3.10. (Preservation of Intervals)** Let $I$ be an interval in $\mathbb{R}$ and suppose a function $f: I \rightarrow \mathbb{R}$ is continuous on $I$. Then $f(I)$ is an interval.

### 6.4 Monotone and Inverse functions on intervals

Definition 6.4.1. 
1. $f$ is said to be **increasing on A** if $x_1, x_2 \in A$ and $x_1 \leq x_2$, then $f(x_1) \leq f(x_2)$. It is strictly increasing if $f(x_1) < f(x_2)$
2. Similar definition for decreasing.
3. A function is **(strictly) monotone** if it is either (strictly) increasing or (strictly) decreasing on $A$.

**Theorem 6.4.2.** A monotone function defined on an interval always has one-sided limits. Let $f: I \rightarrow \mathbb{R}$ be increasing on $I$. If $c \in I$ is not an endpoint of $I$, then
1. $\lim\limits_{x \rightarrow c^-} f(x) = \sup \{ f(x) : x \in I, x < c \}$
2. $\lim\limits_{x \rightarrow c^+} f(x) = \inf \{ f(x) : x \in I, x > c \}$
3. $\lim\limits_{x \rightarrow c^-} f(x) \leq f(c) \leq \lim\limits_{x \rightarrow c^+} f(x)$

Remark: If $f$ is increasing and discontinuous at $c$, then $\lim\limits_{x \rightarrow c^-} f(x) < \lim\limits_{x \rightarrow c^+} f(x)$ and the difference is called the **jump** of $f$ at $c$.

**Theorem 6.4.6. (Continuous Inverse Theorem)** Let $I \subseteq \mathbb{R}$ be an interval and $f : I \rightarrow \mathbb{R}$ be a strictly monotone function. If $f$ is continuous on $I$, then its inverse function $f^{-1} : f(I) \rightarrow \mathbb{R}$ is strictly monotone and continuous on $f(I)$. ^d3c9d0

Example: the n-th root function is continuous and strictly increasing on $\mathbb{R}$.

### 6.5 Uniform continuity

Definition 6.5.1. Let $\emptyset \subsetneq A \subseteq \mathbb{R}$. A function $f : A \rightarrow \mathbb{R}$ is said to be **uniformly continuous on** A if for any given $\epsilon > 0$, there exists $\delta = \delta(\epsilon) > 0$ s.t.  $\vert f(x) - f(u) \vert < \epsilon$ for any $x, u \in A$ satisfying $\vert x - u \vert < \delta$.

Remark: 
1. uniformly continuous on $A$ --> continuous on $A$.
2. uniformly continuous on $A$ --> uniformly continuous on any nonempty subset $B$ of $A$.

**Theorem 6.5.3. (Sequential criterion for uniform continuity)** Let $\emptyset \neq A \subseteq \mathbb{R}$ and let  $f : A \rightarrow \mathbb{R}$ be a function. Then the following statements are equivalent:
1. $f$ is uniformly continuous on $A$.
2. For any two sequences $(x_n)$ and $(u_n)$ in $A$ s.t. $x_n - u_n \rightarrow 0$, one has $f(x_n) - f(u_n) \rightarrow 0$.

**Theorem 6.5.5. (Heine-Cantor Theorem)** Suppose that $f : [a,b] \rightarrow \mathbb{R}$ is a continuous function on the closed bounded interval $[a, b]$. Then $f$ is uniformly continuous on $[a, b]$. ^f1540c

**Lipschitz condition**. Let $A$ be a nonempty subset of $\mathbb{R}$ and let $f: A \rightarrow \mathbb{R}$ be a function satisfying the Lipschitz condition on $A$: there exists a constant $K > 0$ s.t. $\vert f(x) - f(y) \vert \leq K \vert x - y \vert$ for all $x, y \in A$. Then $f$ is uniformly continuous on $A$.

Theorem. If $f : A \rightarrow \mathbb{R}$ is uniformly continuous on a subset $A \subseteq \mathbb{R}$ and if $(x_n)$ is a Cauchy sequence in $A$, then $(f(x_n))$ is a Cauchy sequence in $\mathbb{R}$.

**Continuous Extension Theorem.** A function $f$ is uniformly continuous on the interval $(a,b)$ iff it can be defined at the endpoints $a$ and $b$ s.t. the extended function is continuous on $[a,b]$.

### Tutorial Results

- (Tut 8 Q8) If $0 < C < 1$ and $| f(x) - f(y) | \leq C | x - y |$ then there exist a unique point $a$ s.t. $f(a) = a$.
- (Tut 9 Q7) Suppose $f : [a,b] \rightarrow \mathbb{R}$ is continuous and injective on $[a,b]$. Then $f$ is strictly monotone.
- (Tut 10 Q4) If $f$ is uniformly continuous on an interval $I$ and there is a positive number $k$ s.t. $| f(x) | \geq k$ for all $x \in I$, then $1 / f(x)$ is uniformly continuous on $I$.
- (20/21 Sem 1 Q5) If $f$ is a continuous function. Then $f$ is strictly monotone iff $f$ is injective.


## 7 Metric Spaces

### 7.1 Metric Space

Definition 7.1.1. Let $S \neq \emptyset$. A **metric** on the set $S$ is a function $d: S \times S \rightarrow \mathbb{R}$ that satisfies
1. (*Positivity*) $d(x, y) \geq 0$ for all $x, y \in S$
2. (*Definiteness*) $d(x,y) = 0$ iff $x = y$
3. (*Symmetry*) $d(x, y) = d(y, x)$ for all $x, y \in S$
4. (*Triangle inequality*) $d(x,y) \leq d(x, z) + d(z, y)$ for all $x, y, z \in S$.

A **metric space** $(S, d)$ is a set $S$ together with a metric $d$ on $S$. The metric $d$ is also called a **distance function** on $S$.

Remark 7.1.5. Define the **Euclidean distance function** on $\mathbb{R}^n$ as $$d(x,y) = \sqrt{\sum\limits_{i=1}^n(x_i - y_i)^2}$$ for $x = (x_1, \dots, x_n), y = (y_1, \dots, y_n) \in \mathbb{R}^n$. Then $(\mathbb{R}^n, d)$ forms the **$n$-dimensional Eucliean space**.

Let $(S,d)$ be a metric space, and let $A \subseteq S$. The **induced metric** $d_A : A \times A \rightarrow \mathbb {R}$ on $A$ is defined as $d_A(x,y) := d(x,y)$ for all $x, y \in A$. Then $(A, d_A)$ is called a **metric subspace** of $(X, d)$.

**Other metrics on $\mathbb{R}^n$**
1. $d_1(x,y) := \sum\limits_{i=1}^n \vert x_i - y_i \vert$
2. $d_\infty(x,y) := \max\limits_{1\leq i \leq n} \vert x_i - y_i \vert$. -> (actually it is supremum)
3. (discrete metric) $d(x,y) = 0$ if $x = y$ and $d(x,y) = 1$ otherwise.

Remark: In view of the other metrics in $\mathbb{R}^n$, then we often denote the Euclidean metric as $d_2$. 

Exercise 7.1.10. We have $d_\infty(x,y) \leq d_2(x,y) \leq d_1(x,y) \leq n \cdot d_\infty(x,y)$.

### 7.2 Neighborhood, Convergence

Definition 7.2.1. For $\epsilon > 0$, then the **$\epsilon$-neighborhood** of the point $c \in S$ is the set $V_\epsilon(c) = \{ x \in S : d(x, c) < \epsilon \}$.

Definition 7.2.3. A set $U$ is called a **neighborhood** of $x$ if $U$ contains an $\epsilon$-neighborhood of $x$ for some $\epsilon > 0$.

Definition 7.2.6. Let $(x_n)$ be a sequence of points in $(S, d)$. Let $x \in S$. The sequence $(x_n)$ is said to **converge to $x$ in S** (with respect to $d$) if for every $\epsilon > 0$, exists $K = K(\epsilon) \in \mathbb{N}$ s.t. $x_n \in V_\epsilon(x)$ for all $n \geq K$ 

**Remark**: $\lim\limits_{n \rightarrow \infty} x_n = x$ iff $\lim\limits_{n \rightarrow \infty} d(x_n, x) = 0$

### 7.3 Open Sets, Closed Sets

Let $(S, d)$ be a metric space.

Definition 7.3.1. A subset $G$ of $S$ is said to be an **open** set in $S$ if for each $x \in G$, there exists a neighborhood $V$ of $x$ s.t. $V \subseteq G$.

Comment: Roughly speaking, an open set is a set whose "boundary points" are all excluded from the set.

Example: Let $a, b \in \mathbb{R}$ s.t. $a < b$. Then the open interval $(a, b)$ is open.

**Theorem 7.3.5.** Let $a \in S$ and $r > 0$. Then the r-neighborhood $V_r(a)$ of $a$ is open in $S$.

**Theorem 7.3.7. (Open Set Properties)** Let $(S, d)$ be a metric space
1. The empty set $\emptyset$ and $S$ are open.
2. Let $\{ G_\lambda : \lambda \in \Lambda \}$ be a collection of open subsets of $S$, i.e. $G_\lambda$ is open for each $\lambda \in \Lambda$. Then $\bigcup\limits_{\lambda \in \Lambda} G_\lambda$ is open.
3. Let $G_1, G_2, \dots, G_n$ be $n$ (finite) open subsets of $S$. Then $\bigcap\limits_{k=1}^n G_k$ is open.

Definition 7.3.10. A subset $F$ of $S$ is said to be an **closed** set in $S$ if the complement $C(F) := S \backslash F$ is open in $S$.

Remark: $G$ is open in $S$ iff $S \backslash G$ is closed in $S$.

Example: 
- The set $\bar{V}_r(a) := \{ x \in S : d(x, a) \leq r \}$ is closed in $S$.
- Let $a, b \in \mathbb{R}$ s.t. $a < b$. Then the closed interval $[a, b]$ is closed.

**Theorem 7.3.15. (Closed Set Properties)** Let $(S, d)$ be a metric space
1. The empty set $\emptyset$ and $S$ are closed.
2. Let $\{ F_\lambda : \lambda \in \Lambda \}$ be a collection of closed subsets of $S$, i.e. $F_\lambda$ is closed for each $\lambda \in \Lambda$. Then $\bigcap\limits_{\lambda \in \Lambda} F_\lambda$ is closed.
3. Let $F_1, F_2, \dots, F_n$ be $n$ (finite) closed subsets of $S$. Then $\bigcup\limits_{k=1}^n F_k$ is closed.

**Theorem 7.3.18. (Characterization of Closed Sets)** Let $F \subseteq S$. The following statements are equivalent:
1. $F$ is closed in $S$.
2. Every convergent sequence $(x_n) \subseteq F$ has its limit in $F$, i.e. one has $\lim\limits_{n \rightarrow \infty} x_n \in F$.

Some additional definition.
- $\mathbb{Q}$ is neither open nor closed.
- A point $x \in \mathbb{R}$ is said to be an **interior point** of $A \subseteq \mathbb{R}$ if there is a neighborhood $V$ of $x$ s.t. $V \subseteq A$.
- A set $A$ is open iff every point of $A$ is an interior point of $A$.
- A point $x \in \mathbb{R}$ is said to be an **boundary point** of $A \subseteq \mathbb{R}$ if everyneighborhood $V$ of $x$ contains points in $A$ and points in $C(A)$.
- A set $A$ is open iff it does not contain any of its boundary points.
- A set $A$ is closed iff it contains all its boundary points.


### 7.4 Continuity in terms of open sets

Context: Let $(S_1, d_1)$ and $(S_2, d_2)$ be metric spaces, and let $A \subseteq S_1$. Let $f : A \rightarrow S_2$ be a function.

Definition 7.4.1. The function $f$ is said to be **continuous** at a point $c \in A$ if for every $\epsilon > 0$, there exists $\delta = \delta(\epsilon, c) > 0$ s.t. $d_2(f(x), f(c)) < \epsilon$ for all $x \in A$ satisfying $d_1(x,c) < \delta$.

Or equivalently: $f(A \cap V_\delta(c)) \subseteq V_{\epsilon}(f(c))$

Definition 7.4.2. Let $f : A \rightarrow B$ be a function and let $G \subseteq B$. Then the **inverse image** of $G$ under $f$ is given by $f^{-1}(G) := \{ x \in A : f(x) \in G \} \subseteq A$. 

Remark: We have $f(f^{-1}(G)) \subseteq G$.

**Theorem 7.4.3. (Global Continuity Theorem)** The following statements are equivalent:
1. $f$ is continuous on $A$.
2. For every *open* set $G \subseteq S_2$, there exists an *open* set $H \subseteq S_1$ s.t. $f^{-1}(G) = A \cap H$

Corollary 7.4.5. A function $f: S_1 \rightarrow S_2$ is continuous on $S_1$ iff the inverse image $f^{-1}(G)$ is open in $S_1$ for every open set $G$ in $S_2$.

Remark: The above corollary also works if I change the word "open" to "closed".

**Theorem 7.4.8. (Sequential Criterion for Continuity)** The following statements are equivalent:
1. $f$ is continuous at $c$.
2. For every sequence $(x_n)$ in $A$ s.t. $x_n \rightarrow c$, one has $f(x_n) \rightarrow f(c)$.

### 7.5. Sequential compactness

Let $(S, d)$ be a metric space.

Definition 7.5.1. A subset $A \subseteq S$ is said to be **bounded** if there exists $x_0 \in S$ and $M > 0$ s.t. $d(x, x_0) \leq M$ for all $x \in A$.

Definition 7.5.4. A subset $A \subseteq S$ is said to be **sequentially compact** if every sequence in $A$ has a convergent subsequence whose limit is in $A$. 

**Theorem 7.5.6.** Suppose a subset $A \subseteq S$ is sequentially compact, then $A$ is closed and bounded in $S$.

**Theorem 7.5.9. (Heine-Borel Theorem)** Let $k \in \mathbb{N}$. Consider the Euclidean $k$-space $(\mathbb{R}^k, d_2)$ where $d_2$ is the Euclidean metric on $\mathbb{R}^k$. Then a subset $A \subseteq \mathbb{R}^k$ is sequentially compact iff $A$ is closed and bounded in $(\mathbb{R}^k, d_2)$

Remark: Generalized version of [[MA2108 Notes#^f1540c|Heine-Cantor Theorem]] by substituting "closed and bounded" with "compact". 

**Theorem 7.5.10.** Continuous functions preserve sequentially compact sets.

**Theorem 7.5.11. (Extreme Value Theorem)** Let $(S, d)$ be a metric space and let $\emptyset \neq A \subseteq S$ be a **sequentially compact** set. Suppose $f : A \rightarrow \mathbb{R}$ be a **continuous** (real-valued) function on $A$. Then there exist $x_1, x_2 \in A$ s.t. $f(x_1) \leq f(x) \leq f(x_2)$ for all $x \in A$.

Corollary 7.5.12. EVT can be generalized to higher dimensions $(\mathbb{R}^k, d_2)$.

### 7.6 Compactness

Definition 7.6.1. Let $(S, d)$ be a metric space and let $A \subseteq S$.
1. An **open cover** of $A$ is a collection $T$ of open subsets of $S$ s.t. $\bigcup\limits_{G \in T} G \supseteq A$.
2. An open cover $T$ of $A$ is said to have a **finite subcover** if there exist finitely many open sets $G_1, G_2, \dots, G_n \in T$ s.t. $G_1 \cup G_2 \cup \dots \cup G_n \supseteq A$.

Definition 7.6.3. A subset $A \subseteq S$ is said to be **compact** in $(S, d)$ if every open cover of $A$ has a finite subcover.

Example:
- Every finite subset of $\mathbb{R}$ is compact
- $[0, \infty)$ and $(0, 1)$ is not compact.

**Theorem 7.6.6.** $A$ is compact iff $A$ is sequentially compact.

Extending [[MA2108 Notes#^d3c9d0|Continuous Inverse Theorem]], we have
**Theorem.** If $K$ is a compact subset of $\mathbb{R}$ and $f : K \rightarrow \mathbb{R}$ is injective and continuous, then $f^{-1}$ is continuous on $f(K)$.

**Some results**

- If $G$ is an open set and $F$ is a closed set, then $G\backslash F$ is an open set and $F \backslash G$ is a closed set.
- If $F$ is a closed subset of a compact set $K$ in $\mathbb{R}$, then $F$ is compact.
- If $K_1$ and $K_2$ are compact sets, then $K_1 \cup K_2$ and $K_1 \cap K_2$ is compact.
- Let $K \neq \emptyset$ be a compact set, then $\inf K$ and $\sup K$ exists and belong to $K$.
- If $f : \mathbb{R} \rightarrow \mathbb{R}$ is continuous, then the set $\{ x \in \mathbb{R} : f(x) < \alpha \}$ is open;  the set $\{ x \in \mathbb{R} : f(x) \leq \alpha \}$ and the set $\{ x \in \mathbb{R} : f(x) = k \}$ is closed.

---

## Appendix

#### 2.6 Finite and Infinite sets

Definition 2.6.0. Let $f : A \rightarrow B$ be a function. Then,
1. $f$ is **injective** if for all $x_1, x_2 \in A$, if $f(x_1) = f(x_2)$, then $x_1 = x_2$.
2. $f$ is **surjective** if $f(A) = B$, i.e. for every $y \in B$, there exists $x \in A$ s.t. $f(x) = y$.
3. $f$ is **bijective** if $f$ is both injective and surjective.

Definition 2.6.1. 
1. A set is **finite**, if it have $n \geq 0$ elements. A set $S$ have $n > 0$ elements iff there is a bijection from $S$ onto the set $\{1, 2, \dots, n\}$ (or from the set $\{1, 2, \dots, n\}$ to $S$).
2. A set $S$ is said to be **denumerable** (or **countably infinite**) if there exists a surjection of $\mathbb{N}$ onto $S$ (or an injection from $S$ onto $\mathbb{N}$).
3. $S$ is countable if it is finite or countably infinite.
4. A set is **infinite** if it is not finite. A set is **uncountable** if it is not countable.

Uniqueness Thm: If $S$ is a finite set, then the numbers of elements in $S$ is a unique number in $\mathbb{N}$. Moreover, the set $\mathbb{N}$ is an infinite set. 

Lemma 2.6.4. Any subset $A$ of $\mathbb{N}$ is countable.

The set $\mathbb{N} \times \mathbb{N}$, $\mathbb{Z}$ and $\mathbb{Q}$ are denumerable. The interval $I = [0,1]$ is uncountable.

Prop 2.6.5. Let $A \subseteq B$
1. If $B$ is finite, then $A$ is finite.
2. If $B$ is countable, then $A$ is countable.

Prop 2.6.6. If $A_m$ is a countable set for each $m \in \mathbb{N}$, then the union $A := \bigcup_{m=1}^{\infty} A_m$ is countable.

Cantor's Thm: If $A$ is any set, then there is no surjection of $A$ onto the set $\pi(A)$ of all subsets of $A$

#### 4.6 Rearrangements of series

Definition. A series $\sum b_n$ is called a **rearrangement** of a series $\sum a_n$ if there is a bijection $f : \mathbb{N} \rightarrow \mathbb{N}$ s.t. $b_n = a_{f(n)}$ for all $n \in \mathbb{N}$.

**Theorem 4.6.2 (Rearrangement Theorem)**. Let $\sum a_k$ be an **absolutely convergent** series. Then, any rearragement $\sum b_k$ of $\sum a_k$ also converges and we have $\sum b_k = \sum a_k$. 

Comment: Riemann showed that a conditionally convergent series can be rearranged s.t. $\sum a_n = c$ for any arbitrary constant $c$

#### 4.7 Why is $e$ irrational?

**Theorem 4.7.1 **
1. $e = \sum \frac{1}{n!}$ -> Proof: Using $\lim \left(1 + \frac{1}{n}\right)^n = e$
2. For each $n \in \mathbb{N}$, $e - \sum\limits_{j=0}^n \frac{1}{j!} \leq \frac{1}{n(n!)}$

**Theorem 4.7.2** The Euler number $e$ is irrational.

#### 6.6 Applications of the notion "uniform continuity" to approximate continuous functions

Definition 6.6.1. Let $I \subseteq \mathbb{R}$ be an interval. Then a function $s: I \rightarrow \mathbb{R}$ is said to be a **step function** if $I$ can be partitioned into a union of finite number of subintervals s.t. $s$ restricts to a constant function on each of these subintervals.

**Theorem 6.6.2.** Let $f: [a,b] \rightarrow \mathbb{R}$ be continuous on the closed bounded interval $[a, b]$. Then for any given $\epsilon > 0$, there exists a step function $s_\epsilon : [a,b] \rightarrow \mathbb{R}$ s.t. $\vert f(x) - s_\epsilon(x) \vert < \epsilon$ for all $x \in [a,b]$.

Definition 6.6.3. A function $g: [a,b] \rightarrow \mathbb{R}$ is **piecewise linear on** $[a,b]$ if the interval $[a,b]$ can be partitioned into a finite number of subintervals s.t. the restriction of $g$ to each subinterval is a linear function on the subinterval.

**Theorem 6.6.4.** Let $f: [a,b] \rightarrow \mathbb{R}$ be continuous on the closed bounded interval $[a, b]$. Then for any given $\epsilon > 0$, there exists a continuous piecewise linear function $g_\epsilon : [a,b] \rightarrow \mathbb{R}$ s.t. $\vert f(x) - g_\epsilon(x) \vert < \epsilon$ for all $x \in [a,b]$.

#### 7.7 Connectedness

Definition 7.7.1. Let $(S, d)$ be a metric space.
1. A subset $A$ of $S$ is **disconnected** if there exist open subsets $G, H$ of $S$ s.t. $G \cap A \neq \emptyset$, $H \cap A \neq \emptyset$, $G \cap H \cap A = \emptyset$ and $A \subseteq G \cup H$.
2. A subset $A$ of $S$ is **connected** if $A$ is not disconnected.

**Theorem 7.7.6.** Consider the metric space $(\mathbb{R}, d)$ where $d$ is the usual metric on $\mathbb{R}$. A subset $A$ of $\mathbb{R}$ is connected iff $A$ is an interval.

**Theorem 7.7.7.** Continuous functions preserve connected sets.

**Theorem 7.7.9. (Intermediate Value Theorem)**. Let $(S, d)$ be a metric space, and let $A \neq \emptyset$ be a connected subset of $S$. Suppose a function $f: A \rightarrow \mathbb{R}$ is continuous on $A$. If $a, b \in A$ and $f(a) < L < f(b)$, then there exists $c \in A$ s.t. $f(c) = L$.










