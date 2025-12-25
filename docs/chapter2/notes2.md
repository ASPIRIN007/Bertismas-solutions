## 2.1 Polyhedra and Convex Sets

!!! info "Key box"
    Section 2.1 sets up the geometry language used throughout LP:

    1. A **polyhedron** is the feasible set of finitely many linear inequalities  
    2. **Bounded vs unbounded** sets (can the feasible region extend to infinity?)  
    3. **Hyperplanes** (equalities) and **halfspaces** (inequalities)  
    4. **Convexity**: the line segment between feasible points stays feasible  
    5. **Convex combinations** and the **convex hull**  
    6. Closure facts (Theorem 2.1): intersections preserve convexity; polyhedra are convex  

---

### Polyhedra (feasible sets of LP constraints)

!!! tip "Def box — Polyhedron"
    A **polyhedron** is any set that can be written as
    $P=\{x\in\mathbb{R}^n \mid Ax \ge b\},$
    i.e., the set of vectors satisfying finitely many linear inequalities.

**Interpretation:** each inequality is a “cut” of the space; the feasible region is what remains after applying all cuts.

---

### Boundedness

!!! tip "Def box — Bounded set"
    A set $S\subseteq\mathbb{R}^n$ is **bounded** if there exists a constant $K$ such that
    $|x_i|\le K$ for every $x\in S$ and each component $i$.

- **Bounded polyhedron:** trapped inside some big box.  
- **Unbounded polyhedron:** you can move infinitely far in some direction while staying feasible.

**Why it matters later:** unboundedness can lead to LPs with no finite optimum (depending on the objective direction).

---

### Hyperplanes and Halfspaces (single linear constraints)

Let $a\neq 0$ and $b\in\mathbb{R}$.

!!! tip "Def box — Hyperplane"
    The **hyperplane** with normal $a$ and offset $b$ is
    $H=\{x\in\mathbb{R}^n \mid a^\mathsf{T}x=b\}.$

!!! tip "Def box — Halfspace"
    The **halfspace** defined by the inequality is
    $S=\{x\in\mathbb{R}^n \mid a^\mathsf{T}x\ge b\}.$

**Key geometric facts**
- The hyperplane $a^\mathsf{T}x=b$ is the **boundary** of the halfspace $a^\mathsf{T}x\ge b$.  
- The vector $a$ is **perpendicular (normal)** to the hyperplane:

  If $x,y\in H$, then $a^\mathsf{T}x=b$ and $a^\mathsf{T}y=b$, so
  $a^\mathsf{T}(x-y)=0,$
  meaning any direction along the hyperplane is orthogonal to $a$.

**Polyhedron viewpoint**
$P=\{x\mid Ax\ge b\}$
is the **intersection of finitely many halfspaces** (one per row of $A$).

---

### Convex Sets (the main structural property)

!!! tip "Def box — Convex set"
    A set $S\subseteq\mathbb{R}^n$ is **convex** if for any $x,y\in S$ and any $\lambda\in[0,1]$,
    $\lambda x + (1-\lambda)y\in S.$
    (Equivalently: the whole line segment between any two points in $S$ lies in $S$.)

**Why convexity matters for LP**
- If $x$ and $y$ are feasible, then any “mix” of them is feasible.  
- This property is fundamental for later results like “an optimum occurs at a corner/extreme point.”

---

### Convex combinations and convex hull

!!! tip "Def box — Convex combination"
    A vector $z$ is a **convex combination** of $x^1,\dots,x^k$ if
    $z=\sum_{i=1}^k \lambda_i x^i,$
    where $\lambda_i\ge 0$ and $\sum_{i=1}^k \lambda_i = 1.$

!!! tip "Def box — Convex hull"
    The **convex hull** of points $x^1,\dots,x^k$ is the set of all their convex combinations:
    $\mathrm{conv}\{x^1,\dots,x^k\}
    =
    \left\{\sum_{i=1}^k \lambda_i x^i \; \middle|\;
    \lambda_i\ge 0,\ \sum_{i=1}^k\lambda_i=1\right\}.$
    It is the **smallest convex set** containing those points.

---

### Theorem 2.1 (closure properties you’ll use repeatedly)

!!! success "Theorem box — Basic convexity facts"
    1. The **intersection** of convex sets is convex.  
    2. Every **polyhedron** is convex.  
       (Halfspaces are convex, and a polyhedron is an intersection of halfspaces.)  
    3. If $S$ is convex and $x^1,\dots,x^k\in S$, then every **convex combination**
       $\sum_{i=1}^k \lambda_i x^i$ lies in $S$.  
    4. The **convex hull** of finitely many points is convex.

!!! note "Proof idea (what to remember)"
    - Halfspace convexity: if $a^\mathsf{T}x\ge b$ and $a^\mathsf{T}y\ge b$, then  
      $a^\mathsf{T}(\lambda x+(1-\lambda)y)
      =\lambda a^\mathsf{T}x+(1-\lambda)a^\mathsf{T}y
      \ge \lambda b+(1-\lambda)b=b.$  
    - Intersections preserve convexity: if the segment stays in each set, it stays in their intersection.

---

!!! info "Section 2.1 — Exam checklist"
    - A feasible set of linear inequalities is a **polyhedron**: $P=\{x\mid Ax\ge b\}$.  
    - Each inequality defines a **halfspace**; equalities define **hyperplanes**.  
    - Polyhedra are **convex** (intersection of convex halfspaces).  
    - **Bounded** means contained in a box; **unbounded** means it extends to infinity.  
    - **Convex combination** and **convex hull** formalize “mixing” feasible points.

## 2.2 Extreme Points, Vertices, and Basic Feasible Solutions

!!! info "Key box"
    Section 2.2 formalizes what a “corner” of a polyhedron means, in three equivalent ways:

    1. **Extreme point** (purely geometric: cannot be written as a nontrivial convex combination)  
    2. **Vertex** (optimization view: unique optimizer for some linear objective)  
    3. **Basic feasible solution (BFS)** (algebraic test: $n$ linearly independent active constraints)  

    Main result: **Extreme points = vertices = BFS** (Theorem 2.2).  
    It also defines **adjacent** basic solutions (sets up simplex “move along an edge”).

---

### 2.2.1 Extreme points

!!! tip "Def box — Extreme point"
    Let $P$ be a convex set (in particular, a polyhedron). A point $x\in P$ is an **extreme point** of $P$ if it cannot be expressed as a nontrivial convex combination of two distinct points of $P$.

    Equivalently: if $y,z\in P$ and $0\le \lambda \le 1$ satisfy
    $x=\lambda y+(1-\lambda)z,$
    then either $x=y$, or $x=z$, or $\lambda\in\{0,1\}$.

**Geometric meaning:** extreme points are the true “corners” — you cannot obtain them by “mixing” two other feasible points.

---

### 2.2.2 Vertices (supporting-hyperplane / LP viewpoint)

!!! tip "Def box — Vertex"
    Let $P$ be a polyhedron. A point $x\in P$ is a **vertex** of $P$ if it is the **unique optimal solution** of *some* linear program with feasible set $P$.

    That is, there exists a vector $c$ such that $x$ is the unique minimizer of
    $\min\{c^\mathsf{T}u \mid u\in P\}.$

**Geometric meaning:** there is a supporting hyperplane (a level set of a linear objective) that touches $P$ **only at** $x$.

---

### 2.2.3 Active constraints and “enough equalities to pin down a point”

Let the polyhedron be written as
$P=\{x\in\mathbb{R}^n \mid a_i^\mathsf{T}x \ge b_i,\ i=1,\dots,m\}.$

At a point $x\in P$, constraint $i$ is **active** if it holds with equality:
$a_i^\mathsf{T}x=b_i.$

!!! info "Terminology — Active set"
    The **active set** at $x$ is the index set
    $I(x)=\{i\in\{1,\dots,m\} \mid a_i^\mathsf{T}x=b_i\}.$

**Key idea:** if the active constraints at $x$ include $n$ *linearly independent* normals, then those equalities determine $x$ uniquely (they “pin down” the point like a corner).

---

### 2.2.4 Basic solutions and basic feasible solutions

!!! tip "Def box — Basic feasible solution (BFS)"
    A feasible point $x\in P$ is a **basic feasible solution** if among the active constraints at $x$, there exist **$n$ linearly independent** constraints.

    (Equivalently: the active constraint normals span $\mathbb{R}^n$.)

!!! note "Remark — Basic solution vs BFS"
    Often one forms a **basic solution** by selecting $n$ linearly independent constraints, solving them as equalities to obtain a unique candidate $x$, and then checking feasibility.
    
    - If the resulting $x$ satisfies *all* constraints, it is a **basic feasible solution**.  
    - If it violates some constraints, it is a **basic solution** but **not feasible**.

!!! warning "Important remark (representation issue)"
    Whether a point is a *basic solution* can depend on how the polyhedron is written (which constraints you include, redundant constraints, etc.).
    
    However, the main theorem below shows that **BFS are the same as extreme points**, so the property “being a BFS” is ultimately geometric (representation-independent).

---

### 2.2.5 Main equivalence theorem

!!! success "Theorem box — Extreme point = vertex = BFS"
    Let $P$ be a polyhedron. For a point $x\in P$, the following are equivalent:

    1. $x$ is a **vertex** of $P$.  
    2. $x$ is an **extreme point** of $P$.  
    3. $x$ is a **basic feasible solution** of $P$.  

**Why this theorem matters**
- It justifies the “corner” viewpoint in three ways:
  - geometry: extreme point,
  - optimization: vertex,
  - algebra: BFS (what algorithms can test and move between).

---

### 2.2.6 Finiteness of basic solutions

!!! note "Key fact — There are finitely many basic solutions"
    A polyhedron defined by finitely many constraints has only **finitely many** ways to choose $n$ linearly independent constraints.
    
    Therefore, the number of **basic solutions** (and hence BFS / extreme points) is **finite**.

---

### 2.2.7 Adjacency (neighbors) and edges

!!! tip "Def box — Adjacent basic solutions"
    Two **distinct** basic solutions are **adjacent** if they share **$n-1$** linearly independent active constraints.

!!! note "Geometric meaning"
    If two **basic feasible solutions** are adjacent, the line segment joining them lies on an **edge** of the polyhedron.
    (This is the geometric backbone of simplex: move from one BFS to an adjacent BFS along an edge.)

---

!!! info "Section 2.2 — Exam checklist"
    - Know the three corner notions:
      - **Extreme point** = cannot be written as a nontrivial convex combination  
      - **Vertex** = unique optimizer for some linear objective  
      - **BFS** = $n$ linearly independent active constraints at the point  
    - Be able to state: **Extreme point ⇔ Vertex ⇔ BFS**.  
    - Know adjacency: share $n-1$ independent active constraints (neighbors along an edge).


## 2.3 Polyhedra in Standard Form

!!! info "Key box"
    Section 2.3 specializes the geometry of Section 2.2 to the **standard form** feasible set:

    1. Standard form polyhedron: $P=\{x\mid Ax=b,\ x\ge 0\}$  
    2. **Basis** and partition into **basic** vs **nonbasic** variables  
    3. Constructing a **basic solution** by setting $n-m$ variables to zero  
    4. **Basic feasible solution (BFS)** = basic solution that also satisfies $x\ge 0$  
    5. A basic solution has at most $m$ nonzero components  
    6. Adjacent bases (differ by one column) correspond to “neighbor” corners (sets up simplex)  
    7. Assuming $\mathrm{rank}(A)=m$ is **no loss of generality** (redundant equalities can be removed)

---

### Standard form feasible set

!!! tip "Def box — Standard form polyhedron"
    A **standard form** feasible set is
    $P=\{x\in\mathbb{R}^n \mid Ax=b,\ x\ge 0\},$
    where $A\in\mathbb{R}^{m\times n}$ and $b\in\mathbb{R}^m$.

!!! note "Standing assumption (used throughout)"
    Often we assume $\mathrm{rank}(A)=m$ (the $m$ equality constraints are linearly independent) and $m\le n$.

---

### Bases and basic variables

Let $A_1,\dots,A_n$ denote the columns of $A$.

!!! tip "Def box — Basis (column basis)"
    A set of indices $B\subseteq\{1,\dots,n\}$ with $|B|=m$ is a **basis** if the columns $\{A_j\}_{j\in B}$ are linearly independent.

!!! info "Notation"
    - The **basis matrix** is $A_B\in\mathbb{R}^{m\times m}$ formed by the columns indexed by $B$.  
    - The remaining indices are $N=\{1,\dots,n\}\setminus B$.  
    - Variables $\{x_j\}_{j\in B}$ are **basic variables**; variables $\{x_j\}_{j\in N}$ are **nonbasic variables**.

---

### Basic solutions

In standard form, the equalities $Ax=b$ are always active, and the only inequalities are $x\ge 0$.
A “corner candidate” is obtained by activating $n-m$ of the nonnegativity constraints, i.e., setting $n-m$ variables to zero.

!!! tip "Def box — Basic solution (associated with a basis $B$)"
    Given a basis $B$ (so $A_B$ is invertible), define a vector $x$ by
    $x_N=0,$
    and
    $A_B x_B=b,$
    i.e.,
    $x_B=A_B^{-1}b.$
    This $x$ is called the **basic solution** associated with $B$.

!!! note "Key property"
    Any basic solution has **at most $m$ nonzero components**, because $x_N=0$ and only the $m$ basic variables can be nonzero.

---

### Basic feasible solutions (BFS)

!!! tip "Def box — Basic feasible solution (BFS)"
    A **basic feasible solution** is a basic solution that is feasible:
    $x\ge 0.$

!!! info "Interpretation"
    - A **basis** always produces a **basic solution** via $x_B=A_B^{-1}b,\ x_N=0$.  
    - That basic solution may be infeasible (some component negative).  
    - If it satisfies $x\ge 0$, it is a **BFS** (a “corner” of $P$).

---

### Bases vs basic solutions (not always one-to-one)

!!! note "Remark"
    Different bases can sometimes lead to the **same** basic solution.
    This typically happens when the resulting BFS has some basic variables equal to zero (degeneracy).
    (Example: if $b=0$, then every basis yields the basic solution $x=0$.)

---

### Adjacency in standard form (sets up simplex moves)

!!! tip "Def box — Adjacent bases"
    Two bases $B$ and $B'$ are **adjacent** if they differ in exactly one index, i.e.,
    $|B\cap B'|=m-1.$

!!! note "Geometric meaning"
    Adjacent bases correspond to swapping **one** basic variable with **one** nonbasic variable.
    When this changes the basic solution, it moves to a neighboring corner along an edge of the feasible set.

---

### Full row rank assumption is no loss of generality

!!! success "Theorem box — Removing redundant equalities"
    Consider $P=\{x\mid Ax=b,\ x\ge 0\}$ and suppose $P$ is nonempty.
    If $\mathrm{rank}(A)=k<m$, then some equality constraints are redundant.
    There exists a matrix $D\in\mathbb{R}^{k\times n}$ with $\mathrm{rank}(D)=k$ and a vector $f\in\mathbb{R}^k$ such that
    $\{x\mid Ax=b,\ x\ge 0\}=\{x\mid Dx=f,\ x\ge 0\}.$

!!! note "Takeaway"
    We can assume $\mathrm{rank}(A)=m$ (independent equality constraints) without changing the feasible set, as long as the feasible set is nonempty.

---

!!! info "Section 2.3 — Exam checklist"
    - Standard form: $P=\{x\mid Ax=b,\ x\ge 0\}$.  
    - Basis $B$: choose $m$ linearly independent columns $\Rightarrow A_B$ invertible.  
    - Basic solution: $x_N=0$, $x_B=A_B^{-1}b$.  
    - BFS: basic solution with $x\ge 0$.  
    - Any basic solution has at most $m$ nonzeros.  
    - Adjacent bases differ by one column (simplex “pivot” idea).  
    - Redundant equalities can be removed $\Rightarrow$ assume $\mathrm{rank}(A)=m$.

