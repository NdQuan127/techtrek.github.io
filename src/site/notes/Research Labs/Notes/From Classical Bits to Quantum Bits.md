---
{"dg-publish":true,"permalink":"/research-labs/notes/from-classical-bits-to-quantum-bits/","tags":["quantum_computing"],"created":"2025-03-13T22:03:50.017+07:00","updated":"2025-03-14T15:56:32.851+07:00"}
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

