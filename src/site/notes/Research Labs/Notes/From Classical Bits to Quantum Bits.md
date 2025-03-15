---
{"dg-publish":true,"permalink":"/research-labs/notes/from-classical-bits-to-quantum-bits/","tags":["quantum_computing"],"created":"2025-02-21T16:35:17.001+07:00","updated":"2025-03-14T17:36:23.668+07:00"}
---

# Classical Bits

- A bit is the basic unit of information, which can exist in one of two distinct states: 0 or 1.
- When multiple bits are used together, they can represent more complex information.
> [!Example]
> - A set of three bits can represent $2^{3}= 8$ distinct states, ranging from 000 to 111.
# Quantum Bits (Qubits)

- For the most part we treat qubits as abstract mathematical objects $\Rightarrow$ it gives us the freedom to construct a general theory of quantum which does not depend upon a specific system for its realization.
> [!Definition] Dirac's notation (Bra-Ket)
> $$\text{Bra: } \langle \psi | \quad \quad \quad \text{Ket: } | \psi \rangle$$
> - The set of vectors in the *bra-representation* = The set of vectors in the *ket-representation*.
> - They form a **dual space**. Each vector in the ket space can find a corresponding vector in the bra space.
## Single-Qubit State

- A single-qubit state can be represented by a two dimensional vector with unit length $$\psi = \begin{bmatrix} \alpha \\ \beta\end{bmatrix} \in \mathbb{C}^2,$$ where $|\alpha|^{2}+ |\beta|^{2} = 1$, satisfies the *normalization constraint*.

> [!Definition] Single-Qubit State
> - A single-qubit state can be represented using Dirac notation: $$|\psi \rangle = \alpha |0 \rangle + \beta |1 \rangle ,$$ where:
> 	- $|0 \rangle = \mid \uparrow \rangle = \begin{bmatrix} 1 \\ 0\end{bmatrix}$ and $|1 \rangle = \mid \downarrow \rangle = \begin{bmatrix} 0 \\ 1\end{bmatrix}$ are two computational (unit) basis states.
> 	- The coefficients $\alpha$ and $\beta$ are referred to as *(probability) amplitudes*. They are complex numbers. When measuring the qubit, we get the result:
> 		- 0 with probability $|\alpha|^2$.
> 		- 1 with probability $|\beta|^2$.

- The special states $| 0 \rangle$ and $| 1 \rangle$ are known as *computational basis states*, and form an orthonormal basis for this vector space.

> [!Remark] Geometric representation.
> - We may rewrite the above equation as: $$|\psi \rangle = e^{i\gamma}\Bigg( \cos \frac{\theta}{2} | 0 \rangle + e^{i\varphi}\sin \frac{\theta}{2}|1\rangle \Bigg),$$ where $\theta, \varphi, \gamma$ are real numbers.
> - We can ignore $e^i\gamma$, because it has *no observable effects*: $$|\psi \rangle =  \cos \frac{\theta}{2} | 0 \rangle + e^{i\varphi}\sin \frac{\theta}{2}|1\rangle.$$ 

- The numbers $\theta$ and $\varphi$ define a point on the unit three-dimensional sphere, often called the ***Bloch sphere***. 
![](https://i.imgur.com/GHoVEAj.png)

> [!Example] Changing basis
> - Representing in the a different basis: $$ |+\rangle = \frac{1}{\sqrt{2}}|0\rangle + \frac{1}{\sqrt{2}}|1\rangle \quad \quad \text{ and } \quad \quad |-\rangle = \frac{1}{\sqrt{2}}|0\rangle - \frac{1}{\sqrt{2}}|1\rangle.$$
> - We can represent $|0\rangle$ and $|1\rangle$ as: $$ |0\rangle = \frac{1}{\sqrt{2}}|+\rangle + \frac{1}{\sqrt{2}}|-\rangle \quad \quad \text{ and } \quad \quad |1\rangle = \frac{1}{\sqrt{2}}|+\rangle - \frac{1}{\sqrt{2}}|-\rangle.$$

> [!Definition] Bra-notation
> - The conjugated transpose of $\psi$, i.e., $\psi^{\dagger}$, is denoted by $\langle \psi |$ with: $$\langle \psi | = \alpha^{*}\langle 0 | + \beta^{*}\langle 1 |,$$ where $\langle 0 | = \begin{bmatrix}1 \\ 0 \end{bmatrix}$ and $\langle 1 | = \begin{bmatrix}0 \\ 1 \end{bmatrix}$.
## Two-Qubit State

- Suppose we have two qubits. If these were two classical bits, then there would be four possible states, 00, 01, 10, 11. 
- Correspondingly, a two qubit system has four *computational basis states* denoted $|00\rangle, |01\rangle, |10\rangle, |11\rangle$. 
- A Hilbert space is a complete linear space with an inner product defined $\Rightarrow$ a generalization of our real 3D space $\Rightarrow$ can loosely regard a Hilbert space as a space with any dimensions which allows complex coefficients.
- We can form a bigger (higher-dimensional) Hilbert space using the **tensor product**.

> [!Leaf] 
> We can see more about tensor product in:
> - [Quantum Linear Algebra I](Quantum%20Linear%20Algebra%20I.md)

> [!Definition] Two-qubit state
> - The two qubits obey the tensor prudct rule can be defined as: $$|\psi \rangle = \alpha_{00}|00 \rangle + \alpha_{01}|01 \rangle + \alpha_{10}|10 \rangle + \alpha_{11}|11 \rangle \in \mathbb{C}^{4}= \mathbb{C}^{2} \otimes \mathbb{C}^{2},$$ where:
> 	- $|00\rangle = \begin{bmatrix} 1 \\ 0 \\ 0 \\ 0\end{bmatrix}$, $|01\rangle = \begin{bmatrix} 0 \\ 1 \\ 0 \\ 0\end{bmatrix}$, $|10\rangle = \begin{bmatrix} 0 \\ 0 \\ 1 \\ 0\end{bmatrix}$ and $|11\rangle = \begin{bmatrix} 0 \\ 0 \\ 0 \\ 1\end{bmatrix}.$
> 	- The coeffcients satisfy the *normalization* condition: $\sum\limits_{x\in\{0, 1\}^{2}}|\alpha_{x}|^{2}= 1.$

> [!Example] Bell state
> - There are four types of Bell states, expressed as: $$\begin{align}
|\phi^+\rangle &= \frac{1}{\sqrt{2}} \bigl( |00\rangle + |11\rangle \bigr),\\[6pt]
|\phi^-\rangle &= \frac{1}{\sqrt{2}} \bigl( |00\rangle - |11\rangle \bigr),\\[6pt]
|\psi^+\rangle &= \frac{1}{\sqrt{2}} \bigl( |01\rangle + |10\rangle \bigr),\\[6pt]
|\psi^-\rangle &= \frac{1}{\sqrt{2}} \bigl( |01\rangle - |10\rangle \bigr).
\end{align} $$
> - Each Bell state is a superposition of two computational basis states in the four-dimensional Hilbert space.
## Multi-Qubit State

- We now generalize the above two-qubit case to the $N$-qubit case with $N > 2$. 
> [!Definition] Multi-qubit State
> - An $N$-qubit state $|\psi \rangle$ is a $2^N$-dimensional vector with $$|\psi \rangle = \sum\limits_{i=1}^{2^{N}} \alpha_{i}|i\rangle \in \mathbb{C}^{2^{N}},$$ where:
> 	- The symbol '$i$' of the computational basis $|i\rangle$ refers to a bit-string with $i \in \{0, 1\}^N$.
> 	- The coefficients satisfy the normalization constraint $\sum\limits_{i=1}^{2^{N}}|\alpha_{i}|^{2}=1$

- For an $N$-qubit system, the computational basis states are represented as $|i\rangle \in \{|0\dots 0 \rangle, |0 \dots 1 \rangle, ..., |1 \dots 1 \rangle\}$, where $i$ is the binary representation of the state index.
- These states form an orthonormal basis of the $2^{N}$-dimensional Hilbert space, satisfying: $$\langle i | j \rangle = \delta_{ij}, \quad \forall i, j \in [2^N].$$
# Overview

- The tables below shows the basis vectors of multi-qubit systems and other informations

| Number of Qubits | Number of basis vectors | Basis Vectors                                                                                                            | Space                                                                  |
| ---------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| 1                | 2                       | $\|0\rangle,  \|1\rangle$                                                                                                | $\mathbb{C}^2$                                                         |
| 2                | 4                       | $\|00\rangle, \|01\rangle, \|10\rangle, \|11\rangle$<br>or<br>$\|0\rangle, \|1\rangle, \|2\rangle, \|3\rangle$<br>       | $\mathbb{C}^4 = \mathbb{C}^2 \otimes \mathbb{C}^2$                     |
| 3                | 8                       | $\|000\rangle, \|001\rangle, \dots, \|111\rangle$<br>or<br>$\|0\rangle, \|1\rangle, \dots, \|7\rangle$                   | $\mathbb{C}^8 = \mathbb{C}^2 \otimes \mathbb{C}^2\otimes \mathbb{C}^2$ |
| $n$              | $2^n$                   | $\|0\dots0\rangle, \|0\dots1\rangle, \dots, \|1\dots1\rangle$<br>or<br>$\|0\rangle, \|1\rangle, \dots, \|2^{n}-1\rangle$ | $\mathbb{C}^{2^n} = \mathbb{C}^2 \otimes \dots \otimes \mathbb{C}^2$   |
