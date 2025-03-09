---
{"dg-publish":true,"permalink":"/research-labs/notes/quantum-topological-data-analysis-for-detecting-financial-crashes/","tags":["quantum_computing","topology"]}
---

# What is quantum TDA?
TDA can be used for extracting complex and valuable shape-related summaries of high-dimensional data. However, as the *size of dataset grows*, the *number of simplices increases significantly*, leading to rise in the computational complexity of TDA algorithms ([ref](https://quantum-journal.org/papers/q-2022-11-10-855/)).

Quantum computers have the potential to significantly accelerate TDA algorithms. Lloyd et al. introduced fully quantum TDA algorithm: *quantum random access memory (qRAM), Grover's search algorithm. and quantum phase estimation (QPE)*([ref](https://www.nature.com/articles/ncomms10138)). In this approach, classical data is first loaded and encoded into the quantum amplitudes of quantum state via qRAM. Grover's algorithm is then employed to construct simplex state, with membership function used to determine whether a given simplex belongs to complex. Finally, the combinatorial Laplacian is constructed, and the Betti numbers-key topological invariants are extracted using QPE.

However, this quantum TDA algorithm is really *costly* for NISQ (noisy intermediate-scale quantum) computers. Even more, qRAM requires tính mạch lạc lượng tử bền vững and *low computational error* to store and process the loaded data.

## Does TDA have applications in finance?
Betti numbers offers valuable insights into the structure and shape of complex data. While their use in finance is still in its *early stages*, they show promise in various apllications, such as *credit risk prediction* ([ref](https://ora.ox.ac.uk/objects/uuid:9f4bed48-1763-486f-acbe-393670fab6bb/files/skw52j939s)), *fraud detection, financial bubble detection* ([ref](https://arxiv.org/abs/2304.06877)), *capturing financial instability* ([ref](https://arxiv.org/pdf/2110.00098)), etc. It can also be used as an unsupervised learning algorithm for *anomaly detection*.

Several studies suggest that Betti numbers serve as effective indicators of market crashes. The zeroth betti number $\beta_0$ is small at the beginning of market crash and increases as the market crash progresses. There is a *giant connected component* in the market just before the crash, and as the market crashed, this *broke up* into *many smaller components*([ref](https://www.mdpi.com/1099-4300/23/9/1211), [ref](https://www.frontiersin.org/journals/physics/articles/10.3389/fphy.2021.572216/full)).

## Explore future directions of quantum TDA

There are several directions where to extend the analysis. Most work on time series analysis has used persistent homology, and more specifically, the $L^P$ norm of persistence landscapes, which can be used to *detect early warning signals* of *imminent market crashes*. Điều này được đề xuất trong nghiên cứu của Gidea và Katz, see [ref](https://arxiv.org/abs/1703.04385).

Analyze financial correlation network and their degree of 
# Detecting financial bubbles by using qTDA
>[!Leaf]
>- Input: a time series of stock price; Output: a time-evolution of topological properties.
>- Preparing point cloud
>	- Apply Taken's embedding
>	- Apply a sliding window for obatining a time varying point-cloud
>- Building Laplacian
>	- Construct the Vietoris-Rips (VR) complex from the point cloud using `GUDHI`
>	- Build the boundary operator of this complex
>	- Build the Laplacian matrix based on the boundary operators, then pad it and rescale it
>- Applying QPE
>	- Use QPE to find the number non-zero eigenvalues of Laplacian matrix. Round up the results and get the Betti numbers
>	- Vary the resolution threshold and obtain a series of Betti numbers, which are Betti curves
>- Detecting financial market crashes
>	- Find the relation between Betti numbers and financial market crashes

## Step 1: Preparing point cloud
Consider time series $X=\{x_0,x_1,...,x_{L-1}\}$ of numerical values of length $L$ as input. We choose an *embedded dimension $N$* and *time delay $d\ge1$*. **Taken's embedding theorem** convert this time series into a *series of $N$-dimensional time-delay*. Each point in the embedded space is defined as
$$z_t=(x_t,x_{t+d},...,x_{t+(N-1)d});$$
$$t=0,1,...,L-1-(N-1)d.$$
Once we have embedded points, we want to track how their geometric structure changes over time. To do this, we apply a sliding window of fixed size $w$ to the embedded vectors:
$$Z^t = \{z_t,z_{t+1},...,z_{t+w-1}\}, \text{ for } t\in\{0,...,K-1\}$$
>[!Tip]
>Following Takens' embedding theorem, transform the `time_series` into a series of $N$-dimensional vectors. Afterward, apply a sliding window to these vectors and obtain a time-varying point cloud.


## Step 2: Building the Simplicial Complex and the Combinatorial Laplacian

### 2.1. Constructing the Vietoris–Rips Complex

To capture the “shape” of our embedded point cloud, we use the **Vietoris–Rips complex**. For a given point cloud (obtained from Takens’ embedding and a sliding window) and a chosen distance threshold ϵ\epsilon, we form simplices as follows:

- **0-simplices:** Each point in the cloud.
- **1-simplices:** An edge between any two points within distance $\epsilon$.
- **2-simplices:** A filled triangle formed when every pair of three points is within $\epsilon$ of one another, and so on.

In practice, libraries like **GUDHI** are used to automatically generate this complex and output a “simplex tree” where simplices are grouped by their dimension.

### 2.2. Defining the Boundary Operator

For a $k$-simplex $s_k = [v_0, v_1, \dots, v_k]$, the **boundary operator** is defined as
$$\partial_k s_k = \sum_{t=0}^{k} (-1)^t \, [v_0, \dots, v_{t-1}, v_{t+1}, \dots, v_k]$$

This formula produces a formal sum of the $(k-1)$-simplices that make up the boundary of $s_k$.
### 2.3. Forming the Combinatorial Laplacian

Using the boundary operators, the combinatorial Laplacian for the $k$-th homology is computed as:
$$\Delta_k = \partial_k^\dagger \, \partial_k + \partial_{k+1} \, \partial_{k+1}^\dagger,$$
where $\partial_k^\dagger$ is the transpose (or conjugate transpose) of $\partial_k$. The null space of $\Delta_k$ directly gives the $k$-th Betti number:
$$\beta_k = \dim \ker (\Delta_k).$$
Before proceeding to quantum steps, the Laplacian is **padded** so that its size becomes $2^q$ (with $q=\lceil \log_2 |S_k| \rceil$) and **rescaled** using an estimate of the maximum eigenvalue $\tilde{\lambda}_{\text{max}}$ (often via the Gershgorin circle theorem). The rescaling is done by forming
$$H = \frac{\delta}{\tilde{\lambda}_{\text{max}}} \tilde{\Delta}_k,$$
and then constructing the unitary operator:
$$U = e^{iH},$$
where $\delta$ is chosen to keep the eigenvalues within $[0, 2\pi)$.

## Step 3: Applying Quantum Phase Estimation (QPE)

### 3.1. Theoretical Background of QPE

Quantum Phase Estimation (QPE) is a quantum algorithm used to determine the phase θ\theta in the eigenvalue equation
$$U |\psi\rangle = e^{i\theta} |\psi\rangle,$$
where $U$ is the unitary operator constructed from the rescaled Laplacian. In our setting, the key insight is that eigenstates corresponding to a zero eigenvalue of the Laplacian yield a phase of zero (since $e^{i \cdot 0} = 1$).
### 3.2. Implementation Overview
1. **State Preparation:**
    - Initialize a set of counting qubits in a superposition (using Hadamard gates).
    - Prepare the target register (which encodes the eigenstates of UU).
2. **Controlled Unitary Operations:**
    - Apply controlled-$U^{2^j}$ gates so that the phase information is transferred to the counting qubits.
3. **Inverse Quantum Fourier Transform (QFT):**
    - Perform an inverse QFT on the counting register to decode the phase information.
4. **Measurement and Betti Estimation:**
    - Measure the counting qubits. If the probability $p(0)$ of measuring the all-zero state is observed, then the fraction of zero eigenvalues (and hence the Betti number) can be estimated as: $$p(0) = \frac{\tilde{\beta}_k}{2^q} \quad \Rightarrow \quad \tilde{\beta}_k = 2^q \cdot p(0).$$
    - Rounding $\tilde{\beta}_k$ gives the final estimate of $\beta_k$.

In practice, quantum computing libraries (such as Qiskit) are used to implement these steps in a quantum circuit.

## Step 4: Detecting Financial Bubbles via Betti Curve Analysis

### 4.1. Constructing the Betti Curves

For each sliding window of the time series, the process above yields Betti numbers as a function of the resolution threshold $\epsilon$. This collection of Betti numbers, when plotted against $\epsilon$, forms a **Betti curve** that characterizes the topology of the market data over time.

### 4.2. Using $L^p$ Norms to Measure Change

To detect abrupt structural changes in the market—potentially signaling a financial bubble—we compute the pairwise distance between Betti curves of consecutive windows. A common choice is the $L^p$ norm, defined as:
$$\|x\|_p = \left( \sum_i |x_i|^p \right)^{1/p}.$$
For example, using the $L^2$ norm, if the distance between the Betti curves of successive windows spikes, it indicates a significant change in the underlying topology of the data, which could correspond to a market bubble or crash.

### 4.3. Practical Implementation

- **Compute Betti Curves:**
    For each window, calculate the Betti numbers (using the quantum or classical method) across a range of ϵ\epsilon values.
- **Normalize and Compare:**
    Normalize the curves if necessary and compute the LpL^p distance between successive curves.
- **Interpretation:**
    Significant spikes in the $L^p$ distance serve as potential early warning signals of structural transitions in the market data.



