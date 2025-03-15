---
{"dg-publish":true,"permalink":"/research-labs/notes/quantum-linear-algebra-ii/","tags":["#quantum_computing"],"created":"2025-03-13T14:45:57.114+07:00","updated":"2025-03-15T22:15:30.621+07:00"}
---

>[!Leaf]
>For clarity, we start with the definition of block encoding. Based on this we introduce some basic arithmetric rules for block encoding, like the *multiplication, linear combination, and Hadamard product*. Finally, we introduce the *quantum singular value transformation* method, which is a powerful framework that can unify most known quantum algorithms.
# Block encoding

For many computational problems, such as solving linear equations, we need to deal with *non-unitary matrix A*. However, remember that *quantum gates* are **unitary** ($U^T U = 1$). Therefore, if we want to solve these problems on quantum computers, it is essential to consider how to *encode the matrix A into *unitary*. This challenge addressed by **block encoding** technique.

>[!Abstract] Definition (Block encoding, [Gilyén et al., 2019](https://arxiv.org/abs/1806.01838))
>Suppose that A is an $N$-qubit operator, $\alpha, \epsilon \ge 0$ and $\alpha \in \mathbb{N}$. Then we say that $(a+N)$-qubit unitary $U$ is $(\alpha,a,\epsilon)$-block-encoding of $A$ if
>$$\bigl\|\,A \;-\; \alpha\,\bigl(\langle 0|^{\otimes a} \otimes I_{2^N}\bigr)\,U\,\bigl(|0\rangle^{\otimes a} \otimes I_{2^N}\bigr)\bigr\| \;\le\; \varepsilon.$$
>Here, $\bigl\|\cdot\bigr\|$ *represents spectral norm*, i.e., the *largest singular* value of the matrix.


Mọe, khó hiểu vl :))
**Nháp tí xóa**
Nôm na thì đây là cách embed 1 toán tử A vào 1 toán tử unitary U to hơn. Giả sử, có 1 toán tử A tác động lên N qubit, và cho thêm a qubit phụ. Khi đó, 1 ma trận unitary U trên (a+N) qubit được gọi là (\alpha, a, \epsilon)-block encoding của A nếu block thích hợp của U (khi các qubit phụ ở trạng thái $|0 \rangle ^{\otimes a}$ (trạng thái 0 của a qubit phụ)) tương đương với ma trận $A/ \alpha$ trong sai số $\varepsilon$.
Tức là, nếu ban đầu qubit phụ ở trạng thái $|0 \rangle ^{\otimes a}$, thì việc tác động U rồi chiếu trở lại $|0 \rangle ^{\otimes a}$ sẽ cho ta 1 ma trận xập xỉ $A/ \alpha$.


The circuit implementation of block encoding is illustrated in Figure 2.8. The scaled matrix $A/ \alpha$ *interacts* with the state $|\psi \rangle$ if the *first qubit registers* are measured as $|0\rangle$. By definition, we have $\alpha\ge \left\| A  \right\|$ and any unitary $U$ is $(1,0,0)$-block encoding of itself.

![](https://i.imgur.com/oo9uwOQ.png)

>[!Note] Block encoding via the linear combination of unitaries **(LCU)** method
> Suppose that A can be written in the form
> $$A=\sum_{k}\alpha_k U_k$$
> where ${\alpha_k}\in\mathbb{R}$ and $U_k$ are some easily prepared unitaries (such as Pauli strings). Then, LCU method allows us to have access two unitaries,
> 











