# Linear Programming (MA3252)

Bennett Clement

## 1. Intro to LP

LP is a technique for minimizing (or maximizing) **linear** cost function under finitely many equality and inequality constraints. 

$$\large \begin{align*}
\min\limits_{x \in \mathbb{R}^n } \text{ (or max) } \; & c^Tx \\
& A_1x = b_1 \\
& A_2x \leq b_2 \\
\end{align*} $$

### 1.1 Glossary
- $c = (c_1, c_2, \dots, c_n)^T \in \mathbb{R}^n$ is the given **cost vector**. We call $c^Tx$ the **objective function**. Vector $c$ corresponds to direction of increasing cost.
-  A **decision variable** $x_j$ is called **free** if there is no restriction on sign of $x_j$
-  A vector $x = (x_1, x_2, \dots, x_n)^T$ satisfying all constraints is a **feasible solution**
-  The **feasible set** is the set of all feasible solutions.
-  A **feasible** solution $x$ that minimizes the objective function is an **optimal solution**, and its corresponding cost $c^Tx$ is called the **optimal cost** / optimal objective value.

By convention: For a minimization (maximization) problem, the optimal cost (profit) for an **unbounded** feasible region is $-\infty$ ($+\infty$) and for **infeasible** region is $+\infty$ ($-\infty$)

#### LP solutions

An LP can have
1. A unique optimal solution
2. Multiple optimal solutions (bounded or unbounded), but only 1 finite optimal cost
3. Unbounded optimal cost --> indicate missing constraints
4. Infeasible / empty feasible set --> indicate logical inconsistencies

### 1.2 Forms

#### General / Compact Form

In a compact form, each constraint should be written as $a_i^Tx \geq b_i$

Transformations:
1. $a_i^Tx \leq b_i$ --->  $(-a_i)^Tx \geq (-b_i)$
2. $x_j \geq 0$ ---> $(0, 0, \dots, 1, 0, \dots, 0)^Tx \geq 0$
3. $a_i^Tx = b_i$ --->  $a_i^Tx \geq b_i$ and $(-a_i)^Tx \geq (-b_i)$

#### Standard Form

Standard form LPs should have : minimization objective, equality constraints, non-negative variables

Transformations:
1. Eliminate ineq constraints: $a_i^Tx \leq b_i$ --->  $a_i^Tx + s_i = b_i$ with $s_i \geq 0$.
2. Eliminate non-positive vars: $x_i \leq 0$ --> Replace $x_i$ with $-x_i^-$, where $x_i^- \geq 0$.
3. Eliminate free vars: Replace $x_i$ with $(x_i^+ - x_i^-)$, where $x_i^+ = \text{max}\{x_i, 0\}, \; x_i^- = \text{max}\{-x_i, 0\}$

### 1.3 Convexity

A set $S \subset \mathbb{R}^n$ is **convex** if for every $x, y \in S$ and every $\lambda \in [0, 1]$, we have $\lambda x + (1 - \lambda)y \in S$.

$x \in \mathbb{R}^n$ is a **convex combination** of $x_1, \dots x_k \in \mathbb{R}^n$ iff $x = \sum\limits_{i = 1}^k\lambda_ix_i$ where $\lambda_i \geq 0$ and $\sum\limits_{i = 1}^k\lambda_i = 1$.

The **convex hull** of $\{ x_1, \dots, x_k \}$ is the set of points in the convex combination of  $\{ x_1, \dots, x_k \}$.

**Claim**: The feasible region of an LP is a convex set.

A **convex function** satisfies $$ f(\lambda x + (1 - \lambda) y) \leq \lambda f(x) + ( 1 - \lambda) f(y) $$ for all $x, y \in \mathbb{R}^n, \lambda \in [0,1]$.

**Theorem**: Let $f_1, \dots f_m : \mathbb{R}^n \rightarrow \mathbb{R}$ be convex functions. Then the function $$ f(x) := \max\limits_{i = 1, \dots m} f_i(x) $$ is also convex.

Affine function $f(x) = d + c^Tx$ is convex (and also concave) and the piecewise affine function $\max\limits_{i = 1, \dots, m} f_i(x)$ is also convex. Furthermore, we can transform $max(f_1, \dots f_k)$ as the smallest $t$ s.t. $t \geq f_i$ for all $i$

### 1.4 Reformulating to LP

![[linearize-minmin.png]]

## 2 Geometry of LP

A **polyhedron** or polyhedral set is a set of the form $\{ x \in \mathbb{R}^n \mid Ax \leq b \}$, where $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$.

### 2.1 Extreme Point, Vertex, and Basic Feasible Solution (BFS)

All of the following assumes $x \in \mathbb{R}^n$.

A polyhedron is a finite intersection of half spaces (finite vertices)

#### Geometric Definition

A point $x$ is a **extreme point** of $P$ if whenever points $y,z \in P$ and scalar $0 < \lambda < 1$ satisfies $x = \lambda y + (1 - \lambda)z$, then $y = z = x$.

A point $x$ is a **vertex** of $P$ if exists $c \in \mathbb{R}^n$ s.t. $c^T x > c^T y$ for all $y \in P \backslash \{x\}$.

#### Algebraic Definition

If $a_i^Tx' = b_i$, then we say the constraint $a_i^Tx \text{ op } b_i$ is **active/tight** at $x'$.

$x$ is said to be of **rank** $k$ if the span of $\{ a_i \mid a_i^Tx = b_i \}$ has dimension $k$ -> basically satisfies $k$ linearly independent constraints.

$x$ is a **basic** solution if it has rank $n$.

$x$ is a **basic feasible solution** (BFS) of a polyhedron $P$ if:
1. $x \in P$ -> feasible
2. $n$ *linearly independent* constraints are active at $x$. -> basic.

A basic solution $x$ is **degenerate** if more than $n$ constraints are active at $x$.

#### Observation

Given a finite number of linear constraints, there are only a finite number of basic solutions.

**Thm 2.4** Let $P$ be a nonempty polyhedron and $x \in P$. Then $x$ is a vertex $\Longleftrightarrow$ $x$ is an extreme point  $\Longleftrightarrow$ $x$ is a BFS.

### 2.2 BFS for Standard Polyhedra

All of the following assumes $x \in \mathbb{R}^n$.

A **standard form polyhedron** $P = \{ x \in \mathbb{R}^n \mid Ax = b, x \geq 0 \}$, where $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$. The $m$ rows of the matrix $A$ are linearly independent i.e. $m \leq n$. 

Remark: The previous definition is consistent with the standard form LP definition from chapter 1.

#### Basic Solution Construction

A vector $x$ is a **basic** solution of the standard polyhedron iff:
1. $Ax = b$
2. exists indices $S = \{ B(1), B(2), \dots B(m) \}$ s.t.
    1. The **basic** columns $A_{B(1)}, A_{B(2)}, \dots A_{B(m)}$ are linearly independent. The basic columns forms a basis matrix.
    2. **Non-basic variables** $x_i = 0$ for all other $i \notin S$.

$A$ can be partitioned into $( B , N )$, where $B = (A_{B(1)}, A_{B(2)}, \dots A_{B(m)})$.
The basic solution $x$ is of the form $(x_B, x_N)$ where $x_B = B^{-1} b$, $x_N = 0$.

Remark: A basic solution $x$ constructed using above procedure is a BFS  <--> $x \geq 0$.

#### On Adjacency

2 distinct basic solution are **adjacent** iff the corresponding bases share all but one basic column. Geometrically, adjacent BFS are extreme points connected by an edge on the boundary.

### 2.3 General Polyhedra

**Thm 2.8** Suppose $P = \{ x \in \mathbb{R}^n \mid Ax \geq b \} \neq \emptyset$. The following are equivalent:
1. $P$ does not contain a line, i.e. $\nexists x' \in P$ and $d \neq 0 \in \mathbb{R}^n$ s.t. $x' + \theta d \in P$ for all $\theta \in  \mathbb{R}$
2. $P$ has a BFS <--> $P$ has $n$ linearly independent constraints.

Corollary: Every nonempty bounded polyhedron and nonempty standard form polyhedron has at least 1 BFS.

### 2.4 Optimality of BFS

**Thm 2.10** Consider the LP $\min c^Tx$ s.t. $x \in P$, a polyhedron. Suppose $P$ has at least 1 BFS and has an optimal solution, then there is an optimal solution which is a BFS.

This implies that if suffices to check BFS to find optimal solutions.

## 3 The Simplex Method

### 3.1 Developing the Simplex Method

#### Step 1: Finding feasible direction

Definition 3.1. For a polyhedron $P$, and a point $x \in P$, a vector $d$ is a **feasible direction** if $x + \theta d \in P$ for some $\theta > 0$.

A feasible direction $d^j = (d^j_B, d^j_N)$ where $j \in N$ is defined as $d_B^j = - B^{-1}A_j$, $d^j_j = 1$ and $d^j_i = 0$ for all $i \in N \setminus \{j\}$. (Notation note: $A_k$ is the k-th column of A, and $N$ is the set of indices where $A_i$ is a non-basic column for $i \in N$.) 

From the above construction, we have $Ad^j = 0$. See first comment for motivation. 

#### Step 2: Choosing largest multiplier $\theta$

We now need to figure out the largest possible $\bar{\theta}_j > 0$ s.t. $x + \bar{\theta}_j d^j \geq 0$, i.e. $x + \bar{\theta}_j d^j$ is a BFS.

$\bar{\theta}_j = \infty$ if $B^{-1}A_j \leq 0$ -> feasible set unbounded
or
$\bar{\theta}_j = \min \left\{ \frac{(B^{-1}b)_i}{(B^{-1}A_j)_i} \; \vert \; i \in B, (B^{-1}A_j)_i > 0 \right\} = \frac{(B^{-1}b)_l}{(B^{-1}A_j)_l}$

#### Step 3: Calculate new cost

If $x$ is a BFS with a feasible direction $d^j$, $\bar{\theta}_j > 0$, and $\bar{c}_j < 0$, then $x + \bar{\theta}_jd^j$ is also a BFS which improves the objective by $\bar{\theta}_j \bar{c}_j$ where the **reduced cost**  $\bar{c}_j$ (or **rate of cost change** along feasible direction $d^j$) is defined as $\bar{c}_j = c^Td^j = c_j + c_B \cdot d^j_B = c_j - c_B \cdot B^{-1}A_j$

Remark: $\bar{c}_j = 0$ for $j \in B$.

#### Step 4: Stopping condition

Remark 3.7. An optimal solution for minimization LP is reached if $c^T - c^T_BB^{-1}A \geq 0$.

---

**Personal comments:**
1.  $Ad^j = 0$ -> $A(x + \theta d^j) = Ax = b$ -> If $x$ is a BFS, then $x + \theta d^j$ will bring you to an adjacent BFS (where $l$ will become 0 a.k.a. leave basis and $j$ will now become non-zero a.k.a enters basis). The adjacent BFS is on the direction of $d^j$ for some $\theta > 0$.
2. Second step can be informally put as: As $\theta$ gradually increase,  stop on the first intersection with another constraint. For $\bar{\theta}_j$ and $l$ that we choose in step 2, we have $(B^{-1}b)_l + \bar{\theta}_j (B^{-1}A_j)_l = x_l + (\bar{\theta} d^j)_l = 0$. As $j$ enters basis, $l$ leaves basis.

---

Definition 3.4. A BFS is **nondegenerate** if $x_B = B^{-1}b> 0$ i.e. all basic variables are positive.

**Thm 3.5 (Optimality conditions)** Consider a BFS $x$ associated with basis matrix $B$ and let $\bar{c}$ be corresponding vector of reduced costs. 
1. If $\bar{c} \geq 0$, then $x$ is optimal.
2. If $x$ is optimal and **nondegenerate**, then $\bar{c} \geq 0$.

Remark 3.7. In degenerate case, optimal BFS need not have $\bar{c} \geq 0$.


### 3.2 Simplex

#### 3.2.1 Simplex Tableau representation

| Basis | x | Solution |
| --- | --- | --- |
| $\bar{c}$ | $c^T - c_{B}^T B^{-1} A$ | $-c_{B}^T B^{-1} b$ |
| $x_B$ (ordered, top to bottom) | $B^{-1}A$ | $B^{-1}b$ | 

#### 3.2.2 (Primal) Simplex Method

**Start with BFS** (primal feasibility) --> iterates to get primal optimality, i.e. $\bar{c} \geq 0$.

Below is the steps, along with some justification on why the method works.

1. The RHS ( $B^{-1}b$ ) should **always** be non-negative before each iteration. If needed, row multiply by -1 where necessary before the first iteration to satisfy this condition. 
	- Corresponds to the constraint $B^{-1}b = x_B \geq 0$, i.e. $x \geq 0$ <--> $x$ a feasible solution.

2. The basis columns should have $\bar{c}_B = 0$. 
	- Consistent with $\bar{c}_B = c_B^T - c_B^T B^{-1} A_B = 0$

3. Find any negative reduced cost to get entering variable $j$. ( [[MA3252 Notes#Step 1 Finding feasible direction| Step 1]] )
	- This is to find a $y$ s.t. $c^Ty < c^Tx$.

4. Selecting leaving variable $l$. ( [[MA3252 Notes#Step 2 Choosing largest multiplier theta | Step 2]] )
	- Consider variables with positive elements in the "entering variable" column $j$. This ensures $(B^{-1}A_j)_i > 0$.
	- Choose any variable that gives minimum ratio of $\frac{b_i}{v_i} = \frac{(B^{-1}b)_i}{(B^{-1}A_j)_i}$, i.e. $\theta_j$
	- Note that $-d^j_B$ is precisely column $j$, i.e. $B^{-1}A_j$

5. Multiply row $l$ to make pivot 1, i.e. dividing the row by $(B^{-1}A_j)_l$
6. Zero out all other entries, including $\bar{c}$ entry in column $j$.
	- Through step 5 and 6, column $j$ is now of the form $(0, 0, \dots, 1, 0, \dots 0)$, ready to be part of the new basis.
	- Suppose $\bar{B}$ is new basis matrix. We update the $B^{-1}Ax = B^{-1}b$ section by multiplying it with $\bar{B}^{-1}B$ (this multiplication is done implicitly by the row operations). As a result, we end up with  $\bar{B}^{-1}Ax = \bar{B}^{-1}b$
	- Thus, RHS ( previously $x_B$ ) now become $\bar{B}^{-1}b = x_B + \theta_j d^j_B$
	- The reduced cost row is updated accordingly, along with the solution.

7. Update leaving variable with entering variable. Step 5,6,7 completes [[MA3252 Notes#Step 3 Calculate new cost| Step 3]]
8. Repeat steps 3 - 7 until there is no more negative reduced cost. [[MA3252 Notes#Step 4 Stopping condition | Step 4]]

At the end of the iteration, the rightmost column will contain negative of the optimal cost $-c^T_Bx_B = -c^Tx$, and the optimal solution $x_B$. (Remember that $x_N = 0$)

**How to fill in the $\bar{c}$ row?**

1. Find a suitable identity matrix in $A$ and set it as the basic variables.
2. If $c^T_B = 0$, then $\bar{c} = c$.
3. Otherwise, use row operations from $A$ on $c^T$ to zero out $c^T_B$. Use the result as $\bar{c}$.

#### 3.2.3 Two Phase Method

This method solves LP in standard form without a readily available BFS.

**First Phase (Solving the Auxiliary LP)**

Start by transforming standard LP $\{ \min c^Tx \mid Ax = b, x \geq 0 \}$ to Auxiliary LP $\{ \min \sum y \mid A\mathbf{x} + \mathbf{y} = \mathbf{b}, \mathbf{x} \geq 0, \mathbf{y} \geq 0, \mathbf{b} \geq 0 \}$.

1. Ensure $b \geq 0$. Invert row sign if necessary.
2. Add a set of artificial variables $y_i$ to rows without positive slack (to create a starting basis).
3. Get a starting BFS by plugging $x = 0$ and $y = b$. Starting basis is the artificial variables and positive slack variables (an identity matrix).
4. Apply simplex method on auxiliary LP.
5. If the optimal cost in auxiliary LP is zero, a BFS to the original LP is found. Otherwise,  the original LP is infeasible.

**Second Phase**

Now we can solve the original LP with the BFS found in the first phase. Reuse first phase tableau by deleting only the auxiliary variables column. Replace the cost function with the original LP's cost function and do necessary row operations s.t. $c^T_B = 0$.

#### 3.2.4 Big M method

Similar to 2 Phase Method, start by transforming standard LP $\{ \min c^Tx \mid Ax = b, x \geq 0 \}$ to Auxiliary LP $\{ \min c^Tx + M \sum y \mid Ax + y = b, x \geq 0, y \geq 0 \}$ where $M$ is taken to be a very large positive number, then apply simplex method to the Auxiliary LP.

If original LP is feasible and has optimal value, all artificial variables will be driven to 0.

### 3.3 Special Cases

#### 3.3.1 Degeneracy

- A BFS with one or more zero basic variables is **degenerate**.
- Degeneracy reveals that the model has at least 1 redundant constraint at that specific BFS.
- Degeneracy might lead to indefinite cycling in the simplex iteration.
- In general, degeneracy is not a big issue. We should proceed even if we find a degenerate solution during one of the iteration.

#### 3.3.2 Alternative Optima

- LP has more than one optimal solution. Occurs when the objective function is parallel to a binding constraint.
- **Detecting alternative optima**: A tableau has more than one solution if the reduced cost corresponding to any non-basic variable equals to zero (barring degeneracy)
- If an LP has $k \geq 2$ optimal BFS $x^1, x^2, \dots x^k$, then the LP has infinitely many optimal solutions.
- (Remark 3.21) The set of optimal solutions, if it is bounded, is $conv(x^1, x^2, \dots x^k) = \left\{ \sum \lambda_i x^i \mid  \sum \lambda_i = 1, \lambda_i \geq 0 \; \forall i = 1, \dots, k \right \}$

#### 3.3.3 Unbounded Solution

Here we deal with the case:
1. Finite objective, but unbounded optimal set
2. Unbounded objective

**Detecting unboundedness**
- If all constraint coefficients of a non-basic variable $x_j$ are all nonpositive, the solution space is unbounded in the direction $d^j$.
- If in addition to the previous point, the corresponding reduced cost is also negative, i.e. $\bar{c_j} < 0$, then the objective value is $-\infty$.

#### 3.3.4 Infeasibility

- If we use 2 phase method, we will get a positive optimal cost in first phase.
- If we use big-M method, when we reach the stopping condition (all reduced costs are nonnegative), but we have at least one positive auxiliary variable in the optimal solution.

## 4 Duality

Duality allows us to change constraints to variables, and variables to constraints. 

For the following chapter, let's define primal problem (P) as 
$$\begin{align*}
\min \; & c^Tx \\
& Ax = b \\
\end{align*} $$

and its dual problem (D) as 
$$\begin{align*}
\max \; & p^Tb \\
& p^TA = c \\
\end{align*} $$


The table below shows the transformation needed from (P) to its dual (D). Depending on whether (P) is a maximization (right -> left) or minimization (left -> right)

| | minimize | maximize | |
| --- | --- | --- | --- |
| constraints | $\geq$ | $\geq 0$ | variables |
| | $\leq$ | $\leq 0$ | |
| | = | free | |
| variables | $\geq 0$ | $\leq$ | constraints |
| | $\leq 0$ | $\geq$ | |
| | free | = | |

**Thm 4.5**. The dual of the dual is the primal

Remark 4.6. Equivalent primal LPs lead to different but equivalent duals

**Thm 4.8 (Weak Duality)**. The *supremum of maximization* problem objective is at least that of the *infimum of the minimization* problem objective

Suppose the primal LP (P) is a minimization problem. If $x$ is feasible in (P) and $p$ is feasible in (D), then $p^Tb \leq c^Tx$.

**Corollary 4.9** Let $x$ and $p$ be primal and dual feasible, respectively, and $p^Tb = c^Tx$. Then $x$ and $p$ are primal and dual optimal, respectively.

Corollary 4.10. Unboundedness in one problem implies infeasibility in the other. However, infeasibility in one problem might imply either unboundedness or infeasibility in the dual problem.

**Thm 4.11 (Strong duality)**. If an LP has an (finite) optimum, so does its dual. Moreover, both optimal costs are equal.

Remark 4.12. 
1. For a standard form primal LP, an optimal dual is $p^T = c_B^T B^{-1}$ where $B$ is an optimal basis for the primal LP.
2. If there is a basis $B_0$ from *original* LP s.t. $A_{B_0} = I$, then $p^T = c^T_{B_0} - \bar{c}_{B_0}^T$.

Definition. We say that $(x, p)$ satisfies complementary slackness if $p(a^Tx - b) = 0$ and $(c - p^TA)x = 0$.

**Thm 4.16 (Complementary Slackness)**. Let $x$ and $p$ be primal and dual feasible respectively. Then $x$ and $p$ are optimal iff $(x, p)$ satisfies complementary slackness.

Proposition. Suppose $x$ is feasible. Then $x$ is primal optimal iff there is a dual feasible $p$ s.t. $(x, p)$ satisfies complementary slackness.

### Sensitivity analysis of optimal cost w.r.t b (b -> b + $\Delta$)

Let $x$ be a nondegenerate primal optimum of the problem (P), with basis $B$ and corresponding dual optimum $p^T = c^T_B B^{-1}$. If $b$ changes by $\Delta$ s.t. $x'_B = B^{-1}(b + \Delta) \geq 0$ (i.e. $x'_B$ still feasible), then the optimal cost changes by $p^T\Delta$.

In particular, if we let $\Delta = e_i = (0, \dots, 0, 1, 0, \dots, 0)$, then the change in optimal cost is $p_i$. So $p_i$ is interpreted as the **marginal cost** (or **shadow cost**) of $b_i$.

Remark 4.19. Dual variables $p_i$'s can be used to rank the 'requirements' $b_i$ according to their contribution to the objective value.

#### Dual Simplex Method

Starts with **dual feasibility** (a.k.a primal optimality), i.e. $\bar{c} = c^T - p^TA \geq 0$ --> iterates to get primal feasibility, i.e. $x_B = B^{-1}b \geq 0$.

For the dual simplex method, the LP is first transformed to an LP with only $\leq$ constraints so that the slack variables form an identity matrix. Then,

1. The vector $c$ needs to be nonnegative
2. Identify any one entry on the RHS that is negative
3. Identify negative elements in the selected row.
	- If no elements is negative, we have infeasibility in primal LP.
4. Calculate the ratios $\bar{c}_i / \vert v_i \vert$ and select the column with the lowest ratio.
5. Multiply by a factor that makes pivot entry 1.
6. Add appropriate multiple of row to zero out the choosen column
7. Update entering/ leaving variable
8. Repeat steps 2 - 7 until all entry on the RHS is non-negative.


## 5 Sensitivity Analysis

Motivation: to understand if an optimal solution is still optimal under certain changes.

Key Idea: For each case, check that both feasibility, i.e. $B^{-1}b \geq 0$ and optimality conditions, i.e. $c^T \geq 0$ are still satisfied after change.

Notation: For this section, define $p = c^T_B B^{-1}$ and $e_i$ as the i-th unit vector.

Note: All discussion below is based on **minimization LP**.

### 5.1 Change in RHS vector b

Suppose that some component $b_i$ of $b$ is changed to $b_i + \delta_i$.

- Optimality are unaffected. NEED TO CHECK for feasibility: $x_B + \delta_i(B^{-1}e_i) \geq 0$.
- If $b_i + \delta_i$ remains feasible, the optimal cost is affected by $p_i \delta_i$.
- If $\delta_i$ is outside of the range that maintain feasibility of the current basis, we can apply **dual simplex** to find a new optimal solution.

Technique: Change $x_B$ by $B^{-1} \delta$, and apply dual simplex as needed.

### 5.2 Change in cost vector c

Suppose that some component $c_j$ of $c$ is changed to $c_j + \delta_j$.

- Feasibility unaffected. It remains to check for optimality condition
- If $x_j$ is nonbasic, we NEED TO CHECK $\bar{c}_j + \delta_j \geq 0$.
	- When $\delta_j < -\bar{c}_j$, apply **primal simplex** from current BFS.
- If $x_j$ is basic, then the change ($c_B$ to $c_B + \delta e_j$) will affect all reduced costs. The range for $\delta_j$ where the optimal solution remains unchanged:
	- Lower bound: maximum of $\bar{c_i} / (e_jB^{-1}A_i)$ where $e_jB^{-1}A_i < 0$ and $i$ is nonbasic
	- Upper bound: minimum of $\bar{c_i} / (e_jB^{-1}A_i)$ where $e_jB^{-1}A_i > 0$ and $i$ is nonbasic

Technique: Change $\bar{c}_j$ by $\delta_j$, do row operations to make $\bar{c}_B = 0$, and apply primal simplex as needed.

### 5.3 Change in a nonbasic column of A

Suppose that some entry $a_{ij}$ of the nonbasic column $A_j$ is changed to $a_{ij} + \delta_{ij}$

- Feasibility unaffected. Among reduced costs, only $\bar{c}_j$ is affected. 
- NEED TO CHECK: $\bar{c}_j - \delta_{ij}p_i \geq 0$
- When $\delta_{ij}$ is not in range, apply **primal simplex**.

Technique: Change $A_i$ by $B^{-1}\delta$ AND $\bar{c}_i$ by $c_BB^{-1} \delta$ and apply primal simplex as needed.

### 5.4 Adding new variable

Suppose a new variable $x_{n + 1}$, together with a corresponding column $A_{n + 1}$ and cost $c_{n+1}$ is added. This yields the new LP:

$$\begin{align*}
\min \; &\mathbf{c}^T\mathbf{x} &+c_{n+1}x_{n+1} & \\
& A\mathbf{x} &+ A_{n+1}x_{n+1} &= \mathbf{b} \\
& \mathbf{x} \geq 0 & x_{n+1} \geq 0 & \\
\end{align*} $$

- Note that $(x, 0)$ is still a BFS to the new problem.
- NEED TO CHECK optimality, i.e. $\bar{c}_{n + 1} \geq 0$. If not satisfied, apply **primal simplex**.

### 5.5 Adding new constraint

Suppose a new constraint $a_{m + 1}^Tx \leq b_{m + 1}$ is added to original LP. This yields the new LP:

$$\begin{align*}
\min \; &\mathbf{c}^T\mathbf{x} & \\
& A\mathbf{x} & &= \mathbf{b} \\
& a_{m+1}^Tx &+ x_{n+1} &= b_{m + 1} \\
& \mathbf{x} \geq 0 & x_{n+1} \geq 0 & \\
\end{align*} $$

- Optimality unaffected. If original solution satisfies new constraint, it remains optimal to the new problem.
- Otherwise, 
	- Add the new constraint to the optimal tableau
	- Use row operations to make $(x_B, x_{n+1})$ an identity matrix.
	- NEED TO CHECK $\bar{c} \geq 0$. If we do not have feasibility, apply **dual simplex** to solve new problem.

## 6 Formulating Network Flow Problems

Formally, a network is a **directed** graph $G = (V, E)$. 
- Let $x_{ij}$ denote the **amount of flow** through edge $(i,j) \in E$. 
- For each node $v \in V$, $b_v$ denotes the external supply / demand. A node is a **supply** node (if $b_v > 0$), a **demand** node (if $b_v < 0$) or a **transshipment** node (if $b_v = 0$). 
- For each edge $(i, j) \in E$, we have $0 \leq x_{ij} \leq u_{ij}$ for some **upper bound (or capacity)** $u_{ij}$. If $u_{ij} = \infty$, then the problem is **uncapacitated**. Otherwise it is **capacitated**.
- Let $c_{ij}$ denotes the **cost** per unit flow on the edge $(i,j)$   

Put in a LP manner, a network flow problem is :

$$\begin{array}{cl}
\min & \mathbf{c}^T\mathbf{x} & \\
\mbox{s.t.} & A\mathbf{x} = \mathbf{b} & \text{... flow balance constraint} \\
& 0 \leq \mathbf{x} \leq \mathbf{u} & \text{... edge capacity constraint }\\
\end{array} $$

Flow balance constraint: Flow out - Flow in = Supply
$A \in \mathbb{R}^{|V| \times |E|}$ is a node-arc incidence matrix, where column corresponding to arc $(i,j)$ has +1 in the row for outbound node $i$ and -1 in the row for inbound node $j$ and 0 otherwise.

### Shortest Path Problem

Problem: Suppose we have a directed graph $G = (V, E)$ and let the **cost** (or length) for each arc $(i, j) \in E$ be $c_{ij}$. Find a shortest path from a node $s \in V$ to a node $t \in V$.
 
In LP formulation:

$$\begin{array}{cl}
\min & \mathbf{c}^T\mathbf{x} & \\
\mbox{s.t.} & A\mathbf{x} = \mathbf{b} \\
& \mathbf{x} \in \{0, 1\}^{|E|} \\
\end{array} $$ 
where $b_s = 1$, $b_t = -1$ and $b_i = 0$ otherwise. 

Furthermore if there are no negative cycles we can relax the condition on $\mathbf{x}$ to be $\mathbf{x} \geq 0$.

In the optimal solution, we will have $x_{ij} = 1$ if arc $(i, j)$ is in the shortest path and 0 otherwise.

Application: Three Jug Puzzle, Dynamic Lot Sizing

#### Dynamic Lot Sizing

Problem: There are $T$ time periods, and for each of these time periods, there are demands $d_i$ to meet. At any time $i$, we can either produce $x_i$ and/or carry $I_{i-1}$ from time $i - 1$ to fulfill $d_i$. Suppose producing $x_i$ items at time $i$ costs $c_ix_i + K_i$ if $x_i > 0$ and 0 otherwise, where $c_i$ is a per-unit production cost and $K_i$ is a fixed setup cost.

Key property:
1. In all periods, we do not both carry inventory from the previous period and produce
2. Each $x_i = \sum\limits_{k = i}^j d_k$ for some $j \geq {i - 1}$. (Note: if $j = i - 1$, then $x_i = 0$). This means the $x_i$ items produced at time $i$ exactly meet demands for periods $i$ upto $j$.

We can formulate this as a straightline graph $G = (V, E)$ where $V = \{ 0, 1, \dots, T \}$ and $E = \{ (i, j) \mid 0 \leq i < j \leq T \}$. Each arc costs $c_{ij}$ which represents the cost to produce at time $i + 1$ (together with setup and holding costs) to meet the demands at time $i + 1, i + 2, \dots, j$. Solving for the shortest path on $G$ will give us the optimal production schedule.

####  The Dual Problem

$$\begin{array}{cl}
\max & p_s - p_t & \\
\mbox{s.t.} & p_i - p_j \leq c_{ij} & \mbox{ for all } (i, j) \in E\\
& \mathbf{p} \mbox { free} \\
\end{array} $$ 

As multiple dual solutions are possible due to translation, we can just set $p_t = 0$ and now we can interpret $p_i$ as the distance from node $i$ to $t$ along the shortest path.

### Max Flow Problem

Objective: Finds the max amount of commodity that can be transported from a source node to a terminal node without exceeding the given **capacity** of any arc in a capacitated network.

Problem: Suppose we have a directed graph $G = (V, E)$ and let $u_{ij} \in [0, \infty)$ be the capacity for each arc $(i, j) \in E$. Find max flow from node $s \in V$ to node $t \in V$.
 
In LP formulation:

$$\begin{array}{cl}
\max & v & \\
\mbox{s.t.} & A\mathbf{x} = \mathbf{b} \\
& 0 \leq \mathbf{x} \leq \mathbf{u} \\
\end{array} $$ 
where $b_s = v$, $b_t = -v$ and $b_i = 0$ otherwise. 

#### The Dual Problem (Min Cut Problem)

- A **cut** is a partition of $V$ into two subsets $S$ and $\bar{S} = V \backslash S$
- An **s-t cut** is a cut s.t. $s \in S$ and $t \in \bar{S}$
- The **capacity** of a cut is the sum of the capacities of forward arcs $(S, \bar{S})$.
- A minimum s-t cut is an s-t cut with minimum capacity.

By the weak duality theorem, the capacity of any cut is an upper bound on the max flow from $S$ to $\bar{S}$.

**Theorem (Max flow - Min cut Theorem)**. The maximum flow is equal to the capacity of a minimum cut.

The dual problem is:

$$\begin{array}{cl}
\min & \mathbf{u}^T\mathbf{z} & \\
\mbox{s.t.} & -y_i + y_j \leq z_{ij} & \mbox{ for all } (i, j) \in E\\
& -y_s + y_t = 1 \\
& \mathbf{p} \mbox { free, }z_{ij} \geq 0 & \mbox{ for all } (i, j) \in E\\\\
\end{array} $$ 

In the problem, the dual variables will satisfy:
1. $y_i = 1$ if node $i$ is in set $S$ of the cut and $y_i = 0$ otherwise.
2. $z_{ij} = 1$ if arc $(i, j)$ contributes to cut capacity, i.e. $i \in S$ and $j \in \bar{S}$ and $z_{ij} = 0$ otherwise.

### Min Cost Flow Problem

Problem: Suppose we have a directed graph $G = (V, E)$. We have a cost $c_{ij}$ and capacity $u_{ij} \in [0, \infty)$ for each arc $(i, j) \in E$ and a supply / demand value $b_i$ for each node $i \in V$. Find the minimum cost flow s.t. supply meets demands and capacity restrictions are satisfied.
 
In LP formulation:

$$\begin{array}{cl}
\min & \mathbf{c}^T\mathbf{x} & \\
\mbox{s.t.} & A\mathbf{x} = \mathbf{b} \\
& 0 \leq \mathbf{x} \leq \mathbf{u} \\
\end{array} $$ 

Remark:
- The Max Flow problem can be transformed into the min cost flow problem by setting $\mathbf{b} = 0$ and adding a new arc $(t, s)$ with $u_{ts} = \infty$. Cost is defined as $c_{ts} = -1$ and $c_{ij} = 0$ otherwise.
- The shortest path problem can be transformed into the min cost flow problem by setting $u_{ij} = 1$, demands as $b_s = 1$, $b_t = -1$ and $b_i = 0$ otherwise. 

## 7 Network Simplex Method

Assumption:
1. $\sum\limits_{i \in V} b_i = 0$
2. Graph is connected

- Construct a **truncated** node-arc incidence matrix $\tilde{A} \in \mathbb{R}^{(n - 1) \times m}$ by taking $n - 1$ rows of $A$. Replace the flow balance constraint $A\mathbf{x} = \mathbf{b}$ by $\tilde{A}\mathbf{x} = \tilde{\mathbf{b}}$ 
- A flow vector $x \in \mathbb{R}^m$ is a **tree solution** of $G = (V, E)$ if 
	1. $\tilde{A}\mathbf{x} = \tilde{\mathbf{b}}$, and
	2. There is a spanning tree with edges $T \subseteq E$ s.t. $x_{ij} = 0$ for all $(i, j) \notin T$.
- A **feasible tree solution** is a tree solution with $\mathbf{x} \geq 0$.

**Theorem 7.2.** The columns corresponding to $n-1$ arcs form a basis of $\tilde{A}$ iff these arcs form a spanning tree.

Steps:
1. Start with any feasible spanning tree $T$.
2. Pick an arc $(i, j) \notin T$ s.t. $\bar{c}_{ij} < 0$. 
	- Entering arc will form a cycle with arcs in $T$. 
	- Using $(i, j)$ as a forward arc in the cycle, calculate $\bar{c}_{ij}$ as the cost around the cycle (put negative signs for arc that is opposite direction).
	- If $\bar{c}_{ij} \geq 0$ for all arcs $(i, j) \notin T$ then we have obtained an optimal solution.
3. Pick a backward arc $(p, q)$ in the cycle with minimum value of $x_{pq}$.
	- If there is no such backward arc, then the problem is unbounded.
4. Update all $x_{kl}$ in the cycle with $+x_{pq}$ if $(k, l)$ is either $(i, j)$ or a forward arc, and $-x_{pq}$ if $(k, l)$ is a backward arc. Essentially, this will swap $x_{pq}$ with $x_{ij}$.

As in LP, a **degenerate** tree solution corresponds when some arc in tree solution is zero.

#### Alternative way to calculating $\bar{\mathbf{c}}$

We can use
1. $p_n = 0$
2. $c_{ij} = p_i - p_j$ for all $(i, j) \in T$.
3. $\bar{c}_{ij} = c_{ij} - (p_i - p_j)$ for all $(i, j) \in E$

---

### Integrality

**Theorem 7.4.** Consider an uncapacitated network flow problem where underlying graph is connected. Then
1. For every basis matrix $B$, $B^{-1}$ has integer entries
2. If $\mathbf{b}$ integral, then every primal basic solution $\mathbf{x}$ is integral.
3. If $\mathbf{c}$ integral, then every dual basic solution $\mathbf{p}$ is integral.





