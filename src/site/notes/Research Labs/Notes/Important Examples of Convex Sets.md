---
{"dg-publish":true,"permalink":"/research-labs/notes/important-examples-of-convex-sets/","tags":["#convex"],"created":"2025-03-03T10:27:38.620+07:00","updated":"2025-03-09T21:23:47.283+07:00"}
---

- Some simple examples:
	- The empty set $\emptyset$, any single point (i.e., singleton) $\{x_0\}$, and the whole space $\mathbb{R}^n$ are affine (hence, convex) subsets of $\mathbb{R}^n$.
	- Any line is affine. If it pass through zero, it is a subspace, hence also a convex cone.
	- A line segment is convex, but not affine (unless it reduces to a point).
	- A ***ray***, which has the form $\{x_{0}+ \theta v \mid \theta \geq 0 \}$, where $v \neq 0$, is convex, but not affine. It is a convex cone if its base $x_{0}$ is $0$.
	- Any subspace is affine and a convex cone (hence convex).
## Hyperplanes and halfspaces

- A ***hyperplane*** is a set of the form $$\{ x \mid a^{T}x = b\},$$where $a \in \mathbb{R}^n$, $a \neq 0$, and $b \in \mathbb{R}$. This is an affine set
![](https://i.imgur.com/X8O5LQQ.png)
- A hyperplane divides $\mathbb{R}^n$ into two ***halfspaces***. A (closed) halfspace is a set of the form $$\{x \mid a^{T}x \leq b \},$$ where $a \neq 0$, i.e., the solution set of one (nontrivial) linear inequality. Halfspaces are convex, but not affine.
![](https://i.imgur.com/iyiK6Rr.png)
- The boundary of the halfspace above is the hyperplane $\{x \mid a^{T}x = b\}$. The set $\{x \mid a^{T}x < b\}$, which is the interior of the halfspace, is called an ***open halfspace***.
## Euclidean balls and ellipsoids

- A ***(Euclidean) ball*** (or just ball) in $\mathbb{R}^n$ has the form $$B(x_{c}, r) = \{x \mid ||x - x_c||_{2}\leq r\} = \{x \mid (x - x_{c})^{T}(x - x_{c}) \leq r^{2}\},$$ where $r > 0$ and $||.||_2$ denotes the Euclidean norm. The vector $x_c$ is the ***center*** of the ball and the scalar $r$ is its *** radius***; $B(x_{c}, r)$ consists of all points within a distance $r$ of the center $x_c$. Another common representation is $$B(x_{c}, r) = \{ x_{c}+ ru \mid ||u||_{2}\leq 1\}$$.
- A Euclidean ball is a convex set.
- A related family of convex sets is the ***ellipsoids***, which have the form $$\mathcal{E} = \{\, x \mid (x - x_c)^{T} P^{-1} (x - x_c) \le 1 \},$$ where $P = P^{T} \succ 0$, i.e., $P$ is symmetric and positive definite. The vector $x_{c}\in \mathbb{R}^n$ is the ***center*** of the ellipsoid. The matrix $P$ determines how far the ellipsoid extends in every direction from $x_c$; the lengths of the semi-axes of $\mathcal{E}$ are given by $\sqrt{\lambda_i}$, where $\lambda_i$ are the eigenvalues of $P$. A ball is an ellipsoid with $P = r^{2}I$. 
![](https://i.imgur.com/Z3ekrVL.png)
- Another common representation of an ellipsoid is $$\mathcal{E} = \{x_{c}+ Au \mid ||u||_{2}\leq 1\}, $$ where $A$ is square and nonsingular. In this representaion we can assume without loss of generality that $A$ is symmetric and positive definite. By taking $A = P^{1/2}$, this gives the ellipsoid defined above. When the matrix $A$ is symmetric positive semidefinite but singular, the set use $A$ is called a ***degenerate ellipsoid***; its affine dimension is equal to the rank of $A$. Degenerate ellipsoids are also convex.
## Norm balls and norm cones

- Suppose $||.||$ is any norm on $\mathbb{R}^n$. From the general properties of norms it can be shown that a ***norm ball*** of radius $r$ and center $x_c$, given by $\{ x \mid ||x - x_{c}|| \leq r\}$, is convex. The ***norm cone*** associated with the norm $||.||$ is the set $$C = \{ (x, t) \mid ||x|| \leq t \} \subseteq \mathbb{R}^{n+1}.$$ It is a convex cone.
> [!Example]
> The ***second-order cone*** is the norm cone for the Euclidean norm, i.e., $$\begin{align} C & = \{(x, t) \in \mathbb{R}^{n + 1} \mid ||x||_{2}\leq t \} \\ & =\Bigg(\begin{bmatrix} x \\ t \end{bmatrix} \begin{bmatrix} x \\ t \end{bmatrix}^{T}\begin{bmatrix} I & 0 \\ 0 & -1 \end{bmatrix}\begin{bmatrix} x \\ t \end{bmatrix} \leq 0, t \geq 0\Bigg)\end{align}$$ It is also called the ***quadratic cone***, since it is defined by a quadratic inequality. It is also called the ***Lorentz cone*** or ***ice-cream cone***.
![|500](https://i.imgur.com/NJ0EHJI.png)
![|500](https://i.imgur.com/NJ0EHJI.p
-ng)
-

## Polyhedra 

- A ***polyhedron (đa diện)*** is defines as the solution set of a finite number of linear equalities and inequalities: $$\mathcal{P} = \{x \mid a_{j}^{T}x \leq b_{j}, j = 1, \dots, m, c_{j}^ {T}x = d_{j}, j = 1, \dots, p \}.$$ 
- A polyhedron is thus the intersection of a finite number of halfspaces and hyperplanes. Affine sets (e.g., subspaces, hyperplanes, lines), rays, line segments, and halfspaces are all polyhedra. It is easily shown that polyhedra are convex sets.
- A bounded polyhedron is sometimes called a ***polytope***, but some authors use the opposite convention.
![](https://i.imgur.com/emTkzGR.png)

- It will be convenient to use the compact notation $$ \mathcal{P} = \{x \mid Ax \succeq b, Cx = d\},$$ where the symbol $\succeq$ denotes *vector inequality* or *componentwise inequality* in $\mathbb{R}^m$: $u \succeq v$ means $u_{i}\leq v_i$ for $i = 1, \dots, m$.
> [!Example]
> The ***nonnegative orthant*** is the set of points with nonnegative components, i.e., $$\mathbb{R}_{+}^{n} = \{x \in \mathbb{R}^{n} \mid x_{i} \geq 0, i = 1, \dots, n\} = \{x \in \mathbb{R}^{n} \mid x \succeq 0\}.$$ The nonegative orthant is a polyhedron and a cone (and therefore called a ***polyhedral cone*).

### Simplexes

- ***Simplexes (Đơn hình)*** are another important family of polyhedra. Suppose the $k + 1$ points $v_{0}, \dots, v_{k}  \in \mathbb{R}^n$ are *affinely independent*, which means $v_{1} - v_{0} , \dots, v_{k} - v_{0}$ are linearly independent. The simplex determined by them is given by $$C = \operatorname{cone}\{v_{0}, \dots, v_{k\}}= \{\theta_{0}v_{0}+ \dots + \theta_{k}v_{k}\mid \theta \succeq 0, \mathbf{1}^{T}\theta = 1\},$$ where $\mathbf{1}$ denotes the vector with all entries one. The affine dimension of this simplex is $k$, so it is sometimes reffered to as a $k$-dimensional simplex in $\mathbb{R}^n$.
> [!Example] *Some common simplexes*
> - A 1-dimensional simplex is a line segment.
> - A 2-dimensional simplex is a triangle (including interior).
> - A 3-dimensional simplex is a tetrahedron. ![](https://i.imgur.com/2iTCeAU.jpeg)
> - The ***unit simplex*** is the $n$-dimensional simplex determined by the zero vector and the unit vector, i.e., 0, $e_{1}, \dots, e_{n} \in \mathbb{R}^n$. It can be expressed as the set of vectors that satisfy $$x \succeq 0, \quad \mathbf{1}^{T}x \leq 1.$$
> - The ***probability simplex*** is the $(n - 1)$-dimensional simplex determined by the unit vectors $e_{1}, \dots , e_{n}\in \mathbb{R}^n$. It is the set of vectors that satisfy $$ x \succeq 0, \quad \mathbf{1}^{T}x = 1.$$
- We can describe the simplex definition above as a polyhedron in the form of the compact notation above.
### Convex hull description of polyhedra

- The convex hull of the finite set $\{v_{1}, \dots, v_{k}\}$ is $$C = \operatorname{cone}\{v_{1}, \dots, v_{k\}}= \{\theta_{1}v_{1}+ \dots + \theta_{k}v_{k}\mid \theta \succeq 0, \mathbf{1}^{T}\theta = 1\}.$$ This set is a polyhedron, and bounded (except in special cases, e.g., a simplex) it is not a simple to express by a set of linear equalities and inequalities. 
- A generalization of this convex hull description is $$\{\theta_{1}v_{1}+ \dots + \theta_{k}v_{k} \mid \theta_{1}+ \dots \theta_{m}= 1, \theta_{i}\geq 0 , i = 1, \dots, k\},$$ where $m \leq k$. Here we consider nonnegative linear combinations of $v_i$, but only the first $m$ coefficients are required to sum to one. Alternatively, we can interpret it as the convex hull of $v_{1}, \dots, v_m$ + the conic hull of the points $v_{m+1}, \dots, v_k$. This set defines a polyhedron, and conversely, every polyhedron can be represented in this form.
## The positive semidefinite cone

- We use the notation $\mathbf{S}^n$ to denote the set of symmetric $n \times n$ matrices, $$\mathbb{S}^{n}= \{ X \in \mathbf{R}^{n\times n} \mid X = X^T\},$$ which is a vector space with dimension $\frac{n(n + 1)}{2}$.
- $\mathbf{S}_{+}^{n}$ denote the set of symmetric positive semidefinite matrices: $$\mathbf{S}_{+}^{n}= \{X \in \mathbf{S}^{n} \mid X \succeq 0\}.$$
-  $\mathbf{S}_{++}^{n}$ denote the set of symmetric positive definite matrices: $$\mathbf{S}_{++}^{n}= \{X \in \mathbf{S}^{n} \mid X \succ 0\}.$$
- The sets $\mathbf{S}_{+}^n$ and $\mathbf{S}_{++}^n$ are convex cones.
> [!Example] *Positive semidefnite cone* in $\mathbf{S}^{2}$
> We have $$X = \begin{pmatrix} x & y \\ y & z \end{pmatrix} \in \mathbf{S}_{+}^{2} \iff x \geq 0,\quad z \geq 0,\quad xz \geq y^2.$$
> ![](https://i.imgur.com/T5SGf62.png)




