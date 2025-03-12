---
{"dg-publish":true,"permalink":"/research-labs/notes/a-first-glimpse-of-quantum-machine-learning/","tags":["quantum_computing"],"created":"2025-03-07T22:18:03.598+07:00","updated":"2025-03-13T00:59:28.886+07:00"}
---

# Quantum Computers

The orgins of quantum computing can be traced back to 1980 when Paul Benioff introduced the *quantum Turing machine*. Since then, several models of quantum computation have *emerged*, including *circuit-based quantum computation*, *one-way quantum computation*, *adiabatic quantum computation*, and *topological quantum computation*. All of them have been shown to be equivalent to the quantum Turing machine, meaning that a perfect implementation of any one of these models can simulate the others with no more than polynomial overhead.

![800](https://i.imgur.com/fXMijR9.png)

However, as a universal computing device, the potential of quantum computers extens well beyond quantum stimulations. In the 1990s, Shor develop *groundbreaking quantum algorithm for large-number factorization*, posing a serious threat to the security of RSA and Diffie-Hellman encryption. In 1996, Grover's algorithm demonstrated a *quadratic speedup* for *unstructured search problems*, a task with broad applications. Since then, the influence of quantum computing has expanded into a wide range of fields, with new quantum algorithms being developed for achieve runtime speedups in areas such as **finance** ([Herman et al., 2023](https://arxiv.org/abs/2307.11230)), **drug design** ([Santagati et al., 2024](https://arxiv.org/abs/2301.04114)), **optimization** ([Abbas et al., 2024](https://arxiv.org/abs/2312.02279)) and **machine learning**.

>[!Tip]
>To refer details quantum computers, you can read more in the following resources:
>- [From Classical Bits to Quantum Bits](From%20Classical%20Bits%20to%20Quantum%20Bits.md)
>- [Quantum Gates](Quantum%20Gates.md)
>

As we will see, the power of quantum computers is determined by two factors: *number of qubits* and *quantum gates*. One commo``nly used metric is the *quantum volume* $V_Q$. Mathematically, quantum volume represents the *maximum size of square quantum circuits* that the computer can successfully implement to achieve *heavy output generation problem*
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

A key milestone in *FQTC*-based QML algorithms is the **quantum linear equations solver**. The **HHL algorithm** provide breakthrough by *reducing runtime complexity* to *poly-logarithmic scaling with matrix size*, given that the matrix is *well-conditioned* and *sparse*.

Another milestone in FQTC-based QML is the **quantum singular value transformation (QSVT)**. QSVT enables *polynomial transformations* of *singular values* of linear operatoer embedded whithin *unitary matrix*.

In addition to advancements in linear equation solving, another promising line of research in FQTC-based QML *focuses* on leveraging quantum computing to *enhance deep neural networkss* rather than traditional ML models. This research track has two main areas to focus.
1. The firt is the accleleration of **DNN optimization**, with notable examples including quantum algorithm for *dissipative diffrential equations* to *expedite (stochastic) gradient descent*, as well as *Quantum Langevin Dynamics* for optimization.
2. The second area of focus on **advancing Transformers** using quantum computing.

## Progress of QML under NISQ 

Unlike FQTC algorithms, *quantum kernel methods* and *QNNs* are flexible and can be effectively adapted to *limited quantum resources* available in NISQ era.

### Quantum learning models and applications

![](https://i.imgur.com/ggwFeVo.png)

From *model architecture perspective*, quantum versions of popular classical models have been developed, including including *quantum support vector machines* (QSVMs), *quantum neural networks* (QNNs), *quantum convolutional neural netwokrs* (QCNNs), *quantum generative adversarial networks* (QGANs), and *quantum transformers*. Some of these *QNN structure* have been validated on real quantum platforms, demonstrating the *feasibility of applying quantum algorithms* to tasks traditionally dominated by classical deep learning. ([Cerezo et al.,2021](https://arxiv.org/abs/2012.09265), [Li and Deng, 2022](https://arxiv.org/abs/2108.13421), [Tian et al.,2023](https://arxiv.org/abs/2206.03066))

From *application perspective*, QML models implemented on NISQ devices has been explored accross diverse field, including fundamental sience, image classification, healthcare, etc. These applications demonstrate the broad potential of QML in the NISQL era, through achieving full quantum advantage in these areas remains an ongoing challenge ([Bharti et al., 2022](https://arxiv.org/abs/2101.08448), [Cerezo et al., 2022](https://arxiv.org/abs/2303.09491))

### Adaption of advanced AI topics to QML

Beyond model design, advanced topics from AI have bee extended to QML, aiming to *enhance the performance and robustness* of diffrent QML models. Example include *quantum architecture search* ([Du et al.,2022](https://arxiv.org/abs/2010.10217)) (the quantum equivalent of neural architecture search), *pruning methods to reduce the complexity of quantum models* ([Wang et al.,2023](https://arxiv.org/abs/2208.14057)).

Other areas of research include *adversarial learning* ([Lu et al., 2020](https://arxiv.org/abs/2001.00030)), *continual learning* ([Jiang et al., 2022](https://arxiv.org/abs/2108.02786)), *differential privacy* ([Watkins et al., 2023](https://arxiv.org/abs/2103.06232)), *distributed learning* ([Du et al., 2022b](https://ieeexplore.ieee.org/document/9775600/)), *federated learning* ([Ren et al., 2023](https://arxiv.org/abs/2306.09912)), and *interpretability within contex of QML* ([Pira and Ferrie,2024](https://arxiv.org/abs/2308.11098)).

### Theoretical foundations

**Quantum learning theory** ([Banchi et al.,2023](https://arxiv.org/abs/2309.11617)) has garnered icreasing attention, aiming to *compare capabilities* of different QML models and to *identify theoretical advantages* of QML over classical ML models.
![](https://i.imgur.com/84o1phx.png)

The **learnability** of QML models can be evaluated across three key dimensions: ==expressivity, trainability, and generalization capabilities==. Below, we provide a brief overview of each measure:
- **Trainability**: This area examines how *the design of QNNs* influences their *convergence properties*, including the impact of system noise and measurement erros on the ability to *converge to local or global minima*.
- **Expressivity**: Researchers investigate how *the number of parameters* and *the structure* of QNNs affect **the size of the hypothesis space** they can represent. A central question is whether QNNs and quantum kernels can *efficiently represent function or patterns* that classical neural networks cannot, and if so, how to quantify this advantage.
- **Generalization**: This focuses on understanding how *the gap* between *training* and *test error* with the size of dataset, the structure of QNNs or quantum kernels, and the number of parameters. The goal is to determine whether QML models can *generalize more effectively* than classical models.

>[!Leaf]
>The combination of advancements in model design, application domains, and theoretical understanding is driving the progress of QML in the NISQ era. Although the field is still in its early stages, the progress achieved thus far provides promising insights into the potential of quantum computing to enhance conventional AI. As quantum hardware continues to evolve, further breakthroughs are expected, potentially unlocking new possibilities for practical QML applications.


