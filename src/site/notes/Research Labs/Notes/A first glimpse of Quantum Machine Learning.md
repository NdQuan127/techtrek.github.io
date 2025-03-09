---
{"dg-publish":true,"permalink":"/research-labs/notes/a-first-glimpse-of-quantum-machine-learning/","tags":["#quantum_computing"]}
---

# Quantum Computers

The orgins of quantum computing can be traced back to 1980 when Paul Benioff introduced the *quantum Turing machine*. Since then, several models of quantum computation have *emerged*, including *circuit-based quantum computation*, *one-way quantum computation*, *adiabatic quantum computation*, and *topological quantum computation*. All of them have been shown to be equivalent to the quantum Turing machine, meaning that a perfect implementation of any one of these models can simulate the others with no more than polynomial overhead.

![800](https://i.imgur.com/fXMijR9.png)

However, as a universal computing device, the potential of quantum computers extens well beyond quantum stimulations. In the 1990s, Shor develop *groundbreaking quantum algorithm for large-number factorization*, posing a serious threat to the security of RSA and Diffie-Hellman encryption. In 1996, Grover's algorithm demonstrated a *quadratic speedup* for *unstructured search problems*, a task with broad applications. Since then, the influence of quantum computing has expanded into a wide range of fields, with new quantum algorithms being developed for achieve runtime speedups in areas such as **finance** ([Herman et al., 2023](https://arxiv.org/abs/2307.11230)), **drug design** ([Santagati et al., 2024](https://arxiv.org/abs/2301.04114)), **optimization** ([Abbas et al., 2024](https://arxiv.org/abs/2312.02279)) and **machine learning**.

>[!Tip]
>To refer details quantum computers, you can read more in the following resources:
>- [Quantum Bit](Quantum%20Bit.md)
>- [Cổng logic quantum](Research%20Labs/Notes/Cổng%20logic%20quantum.md)

As we will see, the power of quantum computers is determined by two factors: *number of qubits* and *quantum gates*. One commonly used metric is the *quantum volume* $V_Q$. Mathematically, quantum volume represents the *maximum size of square quantum circuits* that the computer can successfully implement to achieve *heavy output generation problem*
$$\log_2(V_Q) = \arg\max_{m} \min(m, d(m)).$$
where $m\le N$ is the number of qubits *selected* from the given $N$-qubit quantum computer, and $d(m)$ is the numbers of qubits in the largest square circuits for which we can achieve *heavy output generation* with *probability* $\ge \frac{2}{3}$.  

**Table 1.1: Progress of quantum computers up to December 2024.**

| Date      | $\log_2(V_Q)$ | N   | Manufacturer | System Name |
| --------- | ------------- | --- | ------------ | ----------- |
| Dec, 2024 | 21            | 105 | Google       | Willow      |
| Aug, 2024 | 21            | 56  | Quantinuum   | H2-1        |
| Jul, 2024 | 9             | 16  | IBM          | Heron       |
| Jun, 2023 | 15            | 20  | Quantinuum   | H1-1        |
| Sep, 2022 | 19            | 29  | IBM          | H2          |
| Apr, 2022 | 12            | 20  | Quantinuum   | H1-2        |
| Jul, 2021 | 10            | 20  | Honeywell    | H1          |
| Nov, 2020 | 7             | 10  | Honeywell    | H0          |
| Aug, 2020 | 7             | 15  | IBM          | Falcon r4   |
 
>[!Note]
>Note that *quantum volume* is not the *unique metric* for evaluating the performance of quantum computers. There are several other metrics that assess the power of quantum processors from different perspectives. For instance, **Circuit Layer Operations Per Second (CLOPS)** measures the *computing speed* of quantum computers, reflecting the feasibility of running practical calculations that involve a large number of quantum circuits. Additionally, *effective quantum volume* provides a more nuanced comparison between noisy quantum processors and classical computers, considering factors such as *error rates* and *noise levels*.


>[!Sprout] Quantum computing paradigms
> - **Superconducting Qubits**: This architecture, championed by companies such as IBM and Google, is notable for its scalability and rapid gate operations. The superconducting approach benefits from *well-established fabrication techniques* derived from semiconductor technology, making it a leading candidate for large-scale quantum computing.
> - **Trapped-Ion Systems**: Spearheaded by IonQ, this architecture features *high coherence times, precise qubit control, and full connectivity between qubits*. These properties make it a promising candidate for quantum error correction, a crucial component for fault-tolerant quantum computing.
> - **Rydberg Atom Systems**: Developed by companies such as QuEra, these systems exploit *highly controllable interactions between neutral atoms, allowing for flexible qubit connectivity*. This adaptability is particularly advantageous for quantum simulation and optimization problems.
> - **Integrated Photonic Quantum Computers**: A growing area of interest, these systems leverage *photonic circuits* to perform quantum computations, offering robust error resilience and the potential for high-speed information processing.

![](https://i.imgur.com/eCeE2IO.png)


# Explored tasks in QML

QML research is extensive and can be broadly divided into *four primary sectors*, each defined by the *nature of the computing resources* (whether computing device is quantum (**Q**) or classical (**C**) and the *nature of the data* (whether generated by a classical (**C**) or quantum (**Q**) system). 

![](https://i.imgur.com/Rm57QyB.png)

The four sectors are as follows:
1. **CC Sector**: Refers to *classical data processed* on *classical systems
2. **CQ Sector**: Using *classical ML algorithms* on *classical processors* to analyze *quantum data* collected from from *quantum systems*. Examples include applying classical neural networks to *classify quantum states*, and using *classical regression* models to predict outcomes of quantum experiments.
3. **QC Sector**: Developing *QML algorithms* run on *quantum processors (QPUs)* to process *classical data*. Examples include applying QML algorithms, such as QNN and quantum kernels, to *solve classical machine learning tasks*.
4. **QQ Sector**: Developing *QML algorithms* run on *quantum processors (QPUs)* to process *quantum data*. Examples include using QNN for *quantum state classification* and applying quantum-enhanced algorithms to *stimulate quantum many-body systems.*

# Progress of QML
## Progress of QML under FTQC

