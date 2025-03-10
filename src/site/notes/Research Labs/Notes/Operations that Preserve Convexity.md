---
{"dg-publish":true,"permalink":"/research-labs/notes/operations-that-preserve-convexity/","tags":["convex"],"created":"2025-03-06T11:27:01.831+07:00","updated":"2025-03-09T21:23:59.950+07:00"}
---

## Intersection

- If $S_1$ and $S_1$ are convex, then $S_{1} \cap S_{2}$ is convex. 
- If $S_\alpha$ is convex for every $\alpha \in \mathcal{A}$, then $\bigcap_{\alpha\in\mathcal{A}} S_\alpha$ is convex.
	- Subspaces, affine sets, and convex cones are also closed under arbitrary intersections.
	- Simple example: Polyhedron is the intersection of halfspaces and hyperplanes (which are convex), therefore is convex.
> [!Example]
> - The positive semidefinite cone $\mathbf{S}_{+}^n$ can be expressed as $$\bigcap_{z \neq 0} \{X \in \mathbf{S}^{n} \mid z^{T} X z \geq 0\}.$$ For each $x \neq 0$, $z^{T}X z$ is a (not identically zero) linear function of $X$, so the sets $$\{X \in \mathbf{S}^{n} \mid z^{T} X z \geq 0\}$$ are, in fact, halfspaces in $\mathbf{S}^n$. Thus the positive semidefinite cone is the intersection of an infinite number of halfspaces, and so is convex.

> [!Example]
> We consider the set $$S = \{ x \in \mathbb{R}^{m} \mid |p(t)| \leq 1 \text{ for } |t| \leq \pi / 3\}$$, where $p(t) = \sum_{k=1}^{m}x_{k}\cos kt$. The set $S$ can be expressed as the intersection of an infinite number of *slabs*: $S = \bigcap_{|t| \leq \pi / 3} S_t$, where $$S_{t}= {x \mid -1 \leq (\cos t, \dots, \cos mt)^{T}x \leq 1},$$ and so is convex.
>  ![|500](https://i.imgur.com/UHe7kpr.png) ![|500](https://i.imgur.com/Pis3tIW.png)

## Affine functions

- A function $f: \mathbb{R}^{n} \rightarrow \mathbb{R}^m$ is *affine* if it is a sum of a linear function and a constant, i.e., has the form $f(x) = Ax + b$, where $A \in \mathbb{R}^{m\times n}$ and $b \in \mathbb{R}^m$. 
- Suppose $S \subseteq \mathbb{R}^n$ is convex and $f : \mathbb{R}^{n} \rightarrow \mathbb{R}^m$ is an affine function. Then the image of $S$ under $f$, $$f(S) = \{f(x) \mid x \in S \},$$ is convex.
- Similarly, if $f : \mathbb{R}^{k}\rightarrow \mathbb{R}^n$ is an affine function, the *inverse image* of $S$ under $f$, $$f^{-1}(S) = \{x \mid f(x) \in S\}$$ is convex.
- Two simple examples are *scaling* and *translation*. If $S \subseteq \mathbb{R}^n$ is convex, $\alpha \in \mathbb{R}$, and $a \in \mathbb{R}^n$:
	- $\alpha S = \{\alpha x \mid x \in S \}$ is convex.
	- $S + a = \{x + a \mid x \in S \}$ is convex.
- The *projection* of a convex set onto some of its coordinates is convex: if $S \subseteq \mathbb{R}^{m}\times \mathbb{R}^n$ is convex, then $$ T = \{x_{1}\in \mathbb{R}^{m}\mid (x_{1}, x_{2}) \in S \text{ for some } x_{2}\in \mathbb{R}^n\}$$ is convex.
- If $S_1$ and $S_2$ are convex, then:
	- $S_{1}+ S_{2}= \{x + y \mid x \in S_{1}, y \in S_{2}\}$ is convex (*sum* of two sets).
	- $S_{1} \times S_{2}= \{ (x_{1}, x_2) \mid x \in S_{1}, y \in S_{2}\}$ is convex (direct or Cartesian product). The image of this set under $f(x) = x_{1}+ x_2$ is the sum $S_{1}+ S_2$.
	- $S = \{(x, y_{1}+ y_{2} ) \mid (x, y_{1}) \in S_{1}, (x, y_{2}) \in S_{2},$ is convex (*partial sum* of convex sets).
> [!Example] *Polyhedron*
> - The polyhedron $\{x \mid Ax \succeq b, Cx = d\}$ can be expressed as the inverse image of the Cartesian product of the nonnegative orthant and the origin under the affine function $f(x) = (b - Ax, d - Cx)$: $$\{x \mid Ax \succeq b, Cx = d\} = \{x \mid f(x) \in \mathbb{R}_{+}^{m}\times \{0\}\}.$$

> [!Example] *Solution set of linear matrix inequality*
> - The condition $$A(x) = x_{1}A_{1}+ \dots + x_{n}A_{n}\preceq B,$$ where $B, A_{i}\in \mathbf{S}^m$, is called a ***linear matrix inequality (LMI)*** in $x$.
> - The solution set of a linear matrix inequality, $\{ x \mid A(x) \preceq B\}$, is convex. It is the inverse image of the positive semidefinite cone under the affine function $f: \mathbb{R}^{n}\rightarrow \mathbf{S}^m$ given by $f(x) = B - Ax$.

> [!Example] *Hyperbolic cone*
> - The set $$\{x \mid x^{T}Px \leq (c^{T}x)^{2}, c^{T}x \geq 0 \}$$ where $P \in \mathbf{S}_{+}^n$ and $c \in \mathbf{S}^n$, is convex, since it is the inverse iamge of the second-order cone, $$\{(z, t) \mid z^{T}z \leq t^{2}, t \geq 0 \},$$ under the affine function $f(x) = (P^{1/2}x,c^{T}x)$.

> [!Example] *Ellipsoid*
> - The ellipsoid $$\mathcal{E} = \{ x \mid (x - x_{c})^{T}P^{-1}(x - x_{c}) \leq 1\},$$ where $P \in \mathbf{S}_{++}^n$, is the image of the unit Euclidean ball $\{u \mid ||u||_{2}\leq 1\}$ under the affine mapping $f(u) = P^{-1/2}u+x_c$. (It is also the inverse image of the unit ball under the affine mapping $g(x) = P^{-1/2}(x - x_{c})$.)

## Linear-fractional and perspective functions

### The perspective function

- We define the ***perspective function*** $P: \mathbb{R}^{n+1}\rightarrow \mathbb{R}^n$, with domain $\operatorname{\textbf{dom}} P = \mathbb{R}^{n}\times \mathbb{R}_{++}$, as $$P(z, t) = z / t.$$ The persepective function scales or normalizes vectors so the last component is one, and then drops the last component.  

> [!Remark]
>  - We can interpret the perspective function as the action of a pin-hole camera. A pin-hole camera (in $R^3$) consists of an opaque horizontal plane $x_3 = 0$, with a single pin-hole at the origin, through which light can pass, and a horizontal image plane $x_3 = -1$. An object at $x$, above the camera (i.e., with $x_3 > 0$), forms an image at the point $-(x_1/x_3, x_2/x_3, 1)$ on the image plane. Dropping the last component of the image point (since it is always -1), the image of a point at $x$ appears at $y = -(x_1/x_3, x_2/x_3) = -P(x)$ on the image plane. 
>  ![](https://i.imgur.com/pNczSPI.png)

- If $C \subseteq \operatorname{\textbf{dom}} P$ is convex, then its image $$P(C) = \{P(x) \mid x \in C\}$$ is convex. This result is certainly intuitive: a convex object, viewed through a pin-hole camera, yields a convex image. (Proof in [ConvexOptimization-Boyd](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf))
- The inverse image of a convex set under the perspective function is also convex: if $C \subseteq \mathbb{R}^n$ is convex then $$P^{-1}(C) = \{(x, t) \in \mathbb{R}^{n + 1} \mid x/t\in C, t > 0\}$$is convex. (Proof in [ConvexOptimization-Boyd](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf) )
### Linear-fractional functions

- A ***linear-fractional function*** is formed by composing the perspective function with an affine function. Suppose $g: \mathbb{R}^{n}\rightarrow \mathbb{R}^{m + 1}$ is affine, i.e., $$g(x) = \begin{bmatrix} A  \\  c^{T}  \end{bmatrix}x + \begin{bmatrix}  b  \\  d  \end{bmatrix},$$ where $A \in \mathbb{R}^{m \times n}, b \in \mathbb{R}^{m}, c \in \mathbb{R}^n$, and $d \in \mathbb{R}$. The function $f: \mathbb{R}^{n}\rightarrow \mathbb{R}^m$ given by $f = P \circ g$, i.e., $$f(x) = \frac{Ax + b}{c^{T}x + d}, \quad \operatorname{\textbf{dom}}f = \{x \mid c^{T}x + d > 0\},$$ is called a ***linear-fractional*** (or ***projective***) function.
	- If $c = 0$ and $d > 0$, the domain of $f$ is $\mathbb{R}^n$, and $f$ is an affine function.
	- Affine and linear functions are special cases of linear-fractional function.

> [!Remark] *Projective interpretation*
> - It is often convenient to represent a linear-fractional function as a matrix $$Q = \begin{pmatrix}A & b \\ c^{T}& d \end{pmatrix} \in \mathbb{R}^{(m + 1) \times (n + 1)}$$ that acts on (multiplies) points of form $(x, 1)$, which yields $(Ax + b, c^{T}x + d)$. This result is then scaled or normalized so that its last component is one, which yields $(f(x), 1)$.
> - The linear fractional function then can be expressed as $$f(X) = \mathcal{P}^{-1}(Q\mathcal{P}(x)).$$

- If $C$ is convex and lies in the domain of $f$ (i.e., $c^{T}x + d > 0 $ for $x \in C$), then its image $f(C)$ is convex.
- If $C \subseteq \mathbb{R}^m$ is convex, then the inverse image $f^{-1}(C)$ is convex. 

> [!Example] *Conditional probabilities*
> - Suppose $u$ and $v$ are random variables that take on values in $\{1, \dots, n\}$ and $\{1, \dots, m\}$, respectively, and let $p_{ij}$ denote $\operatorname{\textbf{prob}}(u = i, v = j)$. Then the conditional probability $f_{ij}= \operatorname{\textbf{prob}}(u = i \mid v = j)$ is given by $$f_{ij}= \frac{p_{ij}}{\sum\limits_{k=1}^{n}p_{kj}}.$$ Thus $f$ is obtained by a linear-fractional mapping from $p$.
> - It follows that if $C$ is a convex set of joint probabilities for $(u, v)$, then the associated set of conditional probabilities of $u$ given $v$ is also convex.

- A set $C \subseteq \mathbb{R}^2$ and its image under the linear-fractional function $$f(x) = \frac{1}{x_{1}+ x_{2}+ 1}x \quad \quad \operatorname{\textbf{dom}}f =\{(x_{1}, x_{2}) \mid x_{1}+ x_{2}+ 1 > 0\}.$$![](https://i.imgur.com/XAdn5aB.png)


