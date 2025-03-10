---
{"up":["[[Convex Theory]]"],"related":null,"created":"2025-03-03 08:54:49","tags":["#convex"],"dg-publish":true,"permalink":"/research-labs/notes/affine-and-convex-sets/","dgPassFrontmatter":true}
---

## Line and line segment

- Suppose $x_1 \neq x_2$ are two points in $\mathbb{R}^n$. Points of the form 
$$ y = \theta x_1 + (1 - \theta)x_2$$
where $\theta \in \mathbb{R}$, form the ***line*** passing through $x_1$ and $x_2$. Values of the parameters $\theta$ between 0 and 1 correspond to the (closed) ***line segment*** between $x_1$ and $x_2$. 
- Expressing $y$ in the form $$y = x_2 + \theta (x_1 - x_2)$$
gives another interpretation: $y$ is the sum of the *base point* $x_2$ and the *direction* $x_1 - x_2$ scaled by the parameter $\theta$. As $\theta$ increases from 0 to 1, the point $y$ moves from $x_2$ to $x_1$; for $\theta$ > 1, the point $y$ lies on the line beyond $x_1$.
## Affine sets

- A set $C \subseteq \mathbb{R}^n$ is ***affine*** if the line through any two distinct points in $C$ lies in $C$, i.e., for any $x_{1}, x_{2}, \in C$ and $\theta \in \mathbb{R}$, we have 
$$
\theta x_{1}+ (1 - \theta) x_{2}\in C
$$
- This idea can be generalized to more than two points. We refer to a point of the form $θ_1x_1 + · · · + θ_kx_k$, where $θ_1 + · · · + θ_k = 1$, as an ***affine combination*** of the points $x_1, . . . , x_k$. If $C$ is an affine set, $x_1, . . . , x_k \in C$, and $θ_1 + · · · + θ_k = 1$, then the point $θ_1x_1 + · · · + θ_kx_k$ also belongs to $C$.
- If $C$ is an affine set and $x_0 \in C$, then the set

$$
V = C - x_0 = \{x - x_0 \mid x \in C\}
$$

is a subspace, i.e., closed under sums and scalar multiplication. Thus, the affine set $C$ can be expressed as
$$
C = V + x_{0}= \{ v + x_{0} \mid v \in V\}
$$
i.e., as a subspace plus an offset. The subspace $V$ associated with the affine set $C$ does not depend on the choice of $x_0$, so $x_0$ can be chosen as any point in $C$. We define the dimension of an affine set $C$ as the dimension of the subspace $V = C-x_0$, where $x_0$ is any element of $C$.

> **Remark:** The solution set of a system of linear equations, $C = \{x \mid Ax = b\}$ where $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$, is an affine set. We also have a converse: every affine set can be expressed as the solution set of a system of linear equations.

- The set of all affine combinations of points in some set $C \subseteq R^n$ is called the ***affine hull*** of $C$, and denoted $\mathbf{aff} C$:

$$
\mathbf{aff} C = \{θ_1x_1 + · · · + θ_kx_k \mid x_1, . . . , x_k ∈ C, θ_1 + · · · + θ_k = 1\}.
$$

The affine hull is the smallest affine set that contains $C$, in the following sense: if $S$ is any affine set with $C ⊆ S$, then $\mathbf{aff} C ⊆ S$.
## Affine dimension and relative interior 

- We define the ***affine dimension*** of a set C as the dimension of its affine hull. If affine dimension of a set $C \subseteq \mathbb{R}^n$ is less than $n$, then the set lies in the affine set $\mathbf{aff} C \neq \mathbb{R}^n$.
- We define the ***relative interior*** of the set $C$, denoted as $\mathbf{relint} C$, as its interior relative to $\mathbf{aff} C$: 
$$
\mathbf{relint}C = \{x \in C \mid B(x, r) \cap \mathbf{aff}C \subseteq C \text{ for some } r > 0\}
,$$
where $B(x, r) = \{y \mid ||y - x|| \leq r\}$, the ball of radius $r$ and center $x$. 
- We can then define the ***relative boundary*** of a set $C$ as $\mathbf{cl} C \setminus \mathbf{relint}C$, where $\mathbf{cl} C$ is the closure of $C$
> **Example:** Consider a square in the $(x_1, x_2)$-plane in $R^3$, defined as
$$
C = \{x \in R^3 \mid − 1 ≤ x_1 ≤ 1, −1 ≤ x_2 ≤ 1, x_3 = 0\}.
$$
Its affine hull is the $(x_1, x_2)$-plane, i.e., $\mathrm{aff} C = \{x \in R^3 | x_3 = 0\}$. The interior of $C$ is empty, but the relative interior is
$$
\mathbf{relint} C = \{x \in R^3 \mid − 1 < x_1 < 1, −1 < x_2 < 1, x_3 = 0\}.
$$
Its boundary (in $R^3$) is itself; its relative boundary is the wire-frame outline,
$$
\{x \in R^3 \mid \max\{|x_1|, |x_2|\} = 1, x_3 = 0\}.
$$
## Convex sets

- A set $C$ is ***convex*** if the line segment between any two points in $C$ lies in $C$, i.e., if for any $x_{1}, x_{2} \in C$ and any $\theta$ with $0 \leq \theta \leq 1$, we have
$$
\theta x_{1} + (1 - \theta) x_{2} \in C.
$$
- As with affine sets, it can be shown that a set is convex if and only if it contains every ***convex combination*** of its points. A convex combination of points can be thought of as a *mixture* or *weighted average* of the points, with $\theta_i$ the fraction of $x_i$ in the mixture.
![|500](https://i.imgur.com/LUh21YO.png)

- The ***convex hull*** of a set $C$, denoted $\mathrm{conv} C$ is the set of all convex combinations of points in $C$:
$$
\textbf{conv } C = \left\{ \theta_1 x_1 + \dots + \theta_k x_k \mid x_i \in C, \theta_i \geq 0, \, i = 1, \dots, k, \, \theta_1 + \dots + \theta_k = 1 \right\}.
$$
- $\textbf{conv } C$ is always convex and is the smallest convex set that contains $C$.
![|700](https://i.imgur.com/3FYg1ER.png)
- The idea of a convex combination can be generalized to include infinite sums.
	- Suppose $\theta_1$, $\theta_2$, ... satisfy $$\theta_{i} \geq 0, i = 1, 2, \dots, \quad \quad \sum\limits_{i = 1}^{\infty} \theta_{i}= 1,$$ and $x_{1}, x_{2}, \dots \in C$, where $C \subseteq \mathbb{R}^n$ is convex. Then $$\sum_{i = 1}^{\infty}\theta_{i}x_{i}\in C,$$ if the series converges.
	- More generally, suppose $p: \mathbb{R}^{n}\rightarrow \mathbb{R}$  satisfies $p(x) \geq 0$ for all $x \in C$ and $\int_{C}p(x) dx = 1$, where $C \subseteq \mathbb{R}^{n}$ is convex. Then $$\int_{C}p(x)x dx \in C,$$ if the integral exists.

## Cones

- A set $C$ is called a ***cone***, or ***nonegative homogeneous***, if for every $x \in C$ and $\theta \geq 0$ we have $\theta x \in C$. A set $C$ is a ***convex cone*** if it is convex and a cone, which means that for any $x_{1}, x_{2} \in C$ and $\theta_{1}, \theta_{2}\geq 0$, we have $$\theta_1x_{1}+ \theta_2x_{2}\in C.$$
![](https://i.imgur.com/KT4ATX5.png)
- A point of the form $θ_1x_1 + · · · + θ_kx_k$ with $θ_1, . . . , θ_k ≥ 0$ is called a ***conic combination*** (or a ***nonnegative linear combination***) of $x_1, . . . , x_k$. If $x_i$ are in a convex cone $C$, then every conic combination of $x_i$ is in $C$. Conversely, a set $C$ is a convex cone if and only if it contains all conic combinations of its elements. Like convex (or affine) combinations, the idea of conic combination can be generalized to infinite sums and integrals.
- The ***conic hull*** of a set $C$ is the et of all conic combinations of points in C, i.e., $$\{ \theta_1x_{1}+ \dots + \theta_{k}x_{k}\mid x_{i}\in C, \theta_{i}\geq 0, i = 1, \dots, k\},$$ which is also the smallest convex cone that contains $C$.
![](https://i.imgur.com/RC6SQHT.png)
