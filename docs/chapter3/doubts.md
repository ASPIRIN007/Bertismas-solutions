# Quick fixes for recurring confusions

!!! info "Key box"
    This page is a running “FAQ” of common confusions that come up while reading Bertsimas (LP).  
    I keep the statements **clean**, specify **what is actually meant**, and (when useful) restate the precise definition/theorem-like claim.

---

## 1) “How can a vector $x$ have a rank? It’s not a matrix.”

!!! note "Key box — What’s going on?"
    A **vector** does *not* have a rank (rank is a matrix concept).  
    When the text/notes say “rank of $x$ is $k$”, they almost always mean:
    - the number of **linearly independent active constraints** at $x$, or
    - the rank of some **matrix built from vectors** (e.g., active constraint normals), or
    - the **dimension** of an affine hull/subspace (sometimes said informally as “rank”).

!!! tip "Definition box — Active constraints (inequality form)"
    For $P=\{x\mid a_i^\top x \ge b_i,\ i=1,\dots,m\}$, constraint $i$ is **active** at $x\in P$ if  
    $a_i^\top x=b_i$.

!!! tip "Definition box — Rank at a point (as used in Section 2.5 / 2.8 style arguments)"
    The “rank of $x$” (informal) means:  
    the maximum number $k$ of **linearly independent** constraint normals among the constraints that are active at $x$.

---

## 2) “Why does local optimality imply global optimality in LP?”

!!! tip "Definition box — Convex set"
    A set $S$ is **convex** if for all $x,y\in S$ and all $\lambda\in[0,1]$,  
    $\lambda x+(1-\lambda)y \in S$.

!!! note "Key box — LP convexity fact"
    - The feasible set of an LP is convex (intersection of halfspaces/affine sets).  
    - The objective $c^\top x$ is linear, hence convex.  
    Therefore, if you cannot improve locally (no feasible descent direction), you are globally optimal.

---

## 3) “They say $c^\top y \ge v$ and $c^\top z \ge v$ implies $c^\top y=v$ and $c^\top z=v$. Why?”

!!! tip "Definition box — Optimal value"
    If $P$ is feasible, the **optimal value** is  
    $v=\min\{c^\top x\mid x\in P\}$ (for a minimization LP).

!!! note "Key box — When equality holds"
    For any feasible $y\in P$, we always have $c^\top y\ge v$.  
    If in addition $y$ is **optimal**, then necessarily $c^\top y=v$.  
    Same for $z$.

!!! warning "Common confusion"
    The implication “$c^\top y\ge v$ therefore $c^\top y=v$” is **false** unless you already know $y$ is optimal.

---

## 4) “What do we gain by writing $c^\top y=v$? Isn’t it just choosing $\lambda=1$ so $y=x^*$?”

!!! note "Key box — What we gain"
    In proofs, we usually start with an optimal point $x^*$ and write it as  
    $x^*=\lambda y+(1-\lambda)z$ with $y\neq z$ and $\lambda\in(0,1)$.  
    Linearity gives:
    $c^\top x^*=\lambda c^\top y+(1-\lambda)c^\top z$.
    
    Since $c^\top x^*=v$ and also $c^\top y\ge v$, $c^\top z\ge v$, the only way the convex combination equals $v$ is:
    $c^\top y=v$ and $c^\top z=v$.
    
    This shows **both endpoints are optimal**, which is the whole point (we are not setting $\lambda=1$).

---

## 5) “How does ‘$x^*$ is a corner/extreme point’ solve a contradiction?”

!!! tip "Definition box — Extreme point"
    A point $x^*\in P$ is an **extreme point** if it cannot be written as  
    $x^*=\lambda y+(1-\lambda)z$ with $y,z\in P$, $y\neq z$, and $\lambda\in(0,1)$.

!!! note "Key box — Why corners matter in linear objectives"
    If $x^*$ is optimal and not an extreme point, you can express it as a strict convex combination of two distinct feasible points.  
    Linearity forces those points to also be optimal (same argument as above).  
    Then you can keep decomposing until you reach an optimal **extreme point** (under the “no lines / at least one extreme point exists” assumptions).

---

## 6) “If an LP has $m$ constraints and $n$ variables, what does rank tell us about existence?”

!!! tip "Definition box — Consistency of $Ax=b$"
    The system $Ax=b$ is **consistent** if there exists $x$ such that $Ax=b$.

!!! note "Key box — Equality constraints only"
    For $Ax=b$:
    - $\mathrm{rank}(A)<m$ means the **rows are dependent** (some equalities are redundant *or* inconsistent depending on $b$).  
    - It does **not** automatically mean infeasible.

!!! note "Key box — Standard form feasibility is stricter"
    In standard form $Ax=b,\ x\ge 0$:
    - Even if $Ax=b$ is consistent, there may be **no nonnegative** solution.  
    - Feasibility means: $\exists x\ge 0$ such that $Ax=b$.

---

## 7) “Set $S$ is convex — what exactly does that mean?”

!!! tip "Definition box — Convexity (repeat, because it’s used everywhere)"
    $S$ is convex iff for all $x,y\in S$ and all $\lambda\in[0,1]$,  
    $\lambda x+(1-\lambda)y\in S$.

!!! info "Key box — Geometry"
    Convex means: **the entire line segment** between any two feasible points stays feasible.

---

## 8) “Why do we introduce reduced costs in simplex?”

!!! tip "Definition box — Reduced cost (standard form)"
    For a basis $B$ and nonbasic index $j$, the **reduced cost** is  
    $\bar c_j = c_j - c_B^\top B^{-1}A_j$.

!!! note "Key box — Meaning"
    $\bar c_j$ is the objective’s **rate of change** when you try to increase $x_j$ from $0$ while keeping $Ax=b$ satisfied by adjusting basic variables.

---

## 11) “What is cycling in simplex and how do anticycling rules fix it?”

!!! tip "Definition box — Degenerate BFS"
    A basic feasible solution is **degenerate** if at least one basic variable equals $0$.

!!! tip "Definition box — Cycling"
    **Cycling** means simplex repeats a previously visited **basis** and can loop forever (possible only under degeneracy).

!!! note "Key box — Why it happens"
    Degeneracy can cause $\theta^*=0$ in the ratio test:  
    basis changes but the point $x$ does not move → can return to an old basis.

!!! info "Theorem box — Anticycling idea (informal)"
    If a pivoting rule guarantees **no basis repeats**, then simplex must terminate in finitely many pivots.

!!! note "Key box — Two rules"
    - **Lexicographic pivoting:** tie-breaks so tableau increases lexicographically → no repetition.  
    - **Bland’s rule:** smallest-index entering + smallest-index leaving among ties → no cycling.

---

## 12) “What is the auxiliary-variable (Phase I) method, and why minimize $\sum y_i$?”

!!! tip "Definition box — Phase I (auxiliary LP)"
    For $Ax=b,\ x\ge 0$ (assume $b\ge 0$ after sign changes), introduce $y\ge 0$ and solve:
    $$
    \min \sum_{i=1}^m y_i
    \quad \text{s.t.}\quad
    Ax+y=b,\ x\ge 0,\ y\ge 0.
    $$

!!! info "Theorem box — Phase I feasibility test (core fact)"
    The original LP is feasible **iff** the Phase I optimal value is $0$.

!!! note "Key box — Why"
    - Always-feasible start: $x=0,\ y=b$.  
    - If original feasible, then $(x,0)$ feasible in Phase I → objective $0$.  
    - Objective is $\ge 0$, so optimum is $0$ exactly when we can drive $y$ to $0$.

---

## 13) “Phase I ended with an artificial variable still basic (value 0). What do we do?”

!!! note "Key box — Degenerate cleanup step"
    If some artificial $y_\ell$ is basic with value $0$ at the end of Phase I:

    - If the entire $\ell$-th row has zeros in the original-variable columns, the corresponding equality is **redundant** → drop that constraint row.
    - Otherwise, pivot in an original variable with a nonzero entry in that row so that $y_\ell$ leaves the basis.

---

## 14) “Big-$M$ vs two-phase simplex — what’s the difference?”

!!! tip "Definition box — Big-$M$ objective"
    Solve one LP:
    $$
    \min\ c^\top x + M\sum_{i=1}^m y_i
    \quad \text{s.t.}\quad
    Ax+y=b,\ x\ge 0,\ y\ge 0,
    $$
    where $M$ is “very large”.

!!! note "Key box — Comparison"
    - **Two-phase:** clean and numerically stable in practice.  
    - **Big-$M$:** conceptually one phase, but large $M$ can cause numerical issues (unless treated symbolically as in textbooks).

---

## 15) “Why add the convexity constraint $e^\top x=1$ in the geometry section?”

!!! tip "Definition box — Convex combination weights"
    If $x\ge 0$ and $e^\top x=1$, then $x$ acts as weights of a convex combination.

!!! note "Key box — Column geometry meaning"
    With $Ax=b$ and $e^\top x=1$:
    - $b=\sum_i x_i A_i$ means $b$ is in $\mathrm{conv}\{A_i\}$.  
    - $z=c^\top x=\sum_i x_i c_i$ means $(b,z)$ is in $\mathrm{conv}\{(A_i,c_i)\}$.

---

## 16) “What is the requirement line?”

!!! tip "Definition box — Requirement line"
    For fixed $b$, the **requirement line** is  
    $\{(b,z)\mid z\in\mathbb{R}\}$ in $\mathbb{R}^{m+1}$.

!!! note "Key box"
    Feasible solutions correspond to intersection points of this vertical line with  
    $H=\mathrm{conv}\{(A_i,c_i)\}$, and the optimum is the **lowest** intersection point.

---

## 17) “What is the dual plane, and why is ‘below the plane’ the same as negative reduced cost?”

!!! tip "Definition box — Dual plane (geometry picture)"
    The lifted basic points $(A_{B(i)},c_{B(i)})$ lie on an $m$-dimensional hyperplane in $\mathbb{R}^{m+1}$ (the **dual plane**).

!!! info "Theorem box — Geometric meaning of reduced cost (informal)"
    For minimization, a point $(A_j,c_j)$ lies **below** the dual plane  
    $\Longleftrightarrow$ the reduced cost satisfies $\bar c_j<0$.

!!! note "Key box"
    Reduced cost is a **signed vertical distance** from the dual plane to the candidate lifted point.

---

## 18) “How can simplex be fast in practice if worst-case is exponential?”

!!! note "Key box"
    - Worst-case constructions force simplex to visit exponentially many vertices.  
    - Real LPs often have structure; with good pivot rules, simplex typically needs far fewer pivots.

!!! info "Key box — What theory separates"
    Performance = (work per pivot) + (number of pivots).  
    Revised simplex + sparsity handles the first; the second is where worst-case exponential behavior lives.

---
