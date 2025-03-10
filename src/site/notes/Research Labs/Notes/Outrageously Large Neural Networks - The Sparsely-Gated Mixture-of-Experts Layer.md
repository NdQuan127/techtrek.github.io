---
{"up":["[[Mixture of Experts MOC]]"],"related":null,"created":"2025-03-07 21:59:39","tags":["mixture_of_experts","paper"],"URL":["https://arxiv.org/pdf/1701.06538"],"dg-publish":true,"permalink":"/research-labs/notes/outrageously-large-neural-networks-the-sparsely-gated-mixture-of-experts-layer/","dgPassFrontmatter":true}
---

# Introduction and Related Work
### Conditional Computation

- Various forms of conditional computation have been proposed as a way to increase model capacity without a proportional increase in computational cost:
	- Large parts of a network are active or inactive on a per-example basis.
	- The gating decisions may be binary or sparse and continuous, stochastic or deterministic.
	- Various forms of reinforcement learning and back-propagation are proposed for trarining the gating decisions.
- Challenges:
	- Computing devices (GPUs) faster at arithmetic than at branching.
	- Large batch sizes are needed.
	- Network bandwidth can be a bottleneck
		-  Embedding layers, which can be seen as a form of conditional computation, are handicapped by this very problem. Since the embeddings generally need to be sent across the network, the number of (example, parameter) interactions is limited by network bandwidth instead of computational capacity.
	-  Loss terms may be necessary to achieve the desired level of sparsity per-chunk and/or per example:
		- [Bengio et al, (2015)](https://arxiv.org/pdf/1511.06297) explore three such terms:
			- This term penalizes deviations of each unit’s _average activation_ from a desired target $\tau$:  
			$$L_{b}= \sum\limits_{j}^{n}||\mathbb{E}\{\sigma_{j}\} - \tau||_{2}\quad \quad \quad \text{Minibatch: } L_{b} \approx \sum\limits_{j}^{n}|| \frac{1}{m_{b}}\sum\limits_{i}^{m_{b}}(\sigma_{ij}) - r||_2.$$
			- Second term encourages each _individual example_ to have total activation close to $\tau$. 
			$$L_e =\mathbb{E}_{x}\{|| (\frac{1}{n} \sum_{j=1}^{n}\sigma_{j})-\tau||_2\}\quad\quad\quad \text{Minibatch: } L_e \approx\frac{1}{m_b}\sum_{i=1}^{m_{b}}|| (\frac{1}{n} \sum_{j=1}^{n}\sigma_{ij})-\tau||_2.$$
			- Third term encoureages *variance* in activations across units, discouraging a uniform distribution. 
			$$L_{v}= - \sum\limits_{j}^{n}\operatorname{var}_{i}\{ \sigma_{ij}\} \approx - \sum\limits_{j}^{n} \frac{1}{m_{b}}\sum\limits_{i}^{m_{b}} \Bigg( \sigma_{ij}- \Bigg( \frac{1}{m_{b}}\sum\limits_{i}^{m_{b}} \sigma_{ij} \Bigg) \Bigg)^2.$$
	- Model capacity is most critical for very large datasets.
### Approach: The Sparsely-Gated MoE Layers

- The MoE consists of a number of experts, each a simple feed-forward neural network, and a trainable gating network which selects a sparse combination of the experts to process each input.
![|700](https://i.imgur.com/mtnEph5.png)
- All parts of the network are trained jointly by back-propagation.
### Related Work on MoEs

- Different types of expert architectures has been proposed:
	- SVMs [Collobert et al, 2002](https://proceedings.neurips.cc/paper_files/paper/2001/file/36ac8e558ac7690b6f44e2cb5ef93322-Paper.pdf)
	- Gaussian Processes [Tresp, 2001](https://proceedings.neurips.cc/paper_files/paper/2000/file/9fdb62f932adf55af2c0e09e55861964-Paper.pdf) [Theis and Bethge, 2015](https://proceedings.neurips.cc/paper/2015/file/2b6d65b9a9445c4271ab9076ead5605a-Paper.pdf) [Deisenroth and Ng](https://proceedings.mlr.press/v37/deisenroth15.pdf)
	- Dirichlet Process [Shahbaba and Neal, 2009](https://www.jmlr.org/papers/volume10/shahbaba09a/shahbaba09a.pdf)
	- Deep networks
- Other work focused on different expert configurations:
	- Hierarchical structure [Yao et al, 2009](https://proceedings.neurips.cc/paper_files/paper/2009/file/a86c450b76fb8c371afead6410d55534-Paper.pdf)
	- Infinite numbers of experts [Rasmussen and Ghahramani, 2002](https://proceedings.neurips.cc/paper_files/paper/2001/file/9afefc52942cb83c7c1f14b2139b09ba-Paper.pdf)
	- Adding experts sequentially [Aljundi et al, 2006](https://arxiv.org/abs/1611.06194)
	- Ensemble model [Garmash and Monz, 2016](https://aclanthology.org/C16-1133.pdf)
# The Structure of the Mixture-of-Experts Layer

- MoE layer consists of :
	- $n$ "expert networks": $E_{1}, \dots, E_{n}$ - which are neural networks with their own parameters.
	- a "gating network" $G$ - output is a sparse $n$-dimensional vector.
- The output $y$ of the MoE module: $$y = \sum\limits_{i=1}^{n}G(x)_{i}E_{i}(x),$$ where $G(x)$ and $E_{i}(x)$ are the output of the gating network and the output of the $i$-th expert network for a given input $x$.
	- If $G(x)_{i}= 0$ then we dont need to compute $E_{i}(x)$
	- Can reduce branching factor by using hierarchical MoE.

### Gating Network

- **Softmax Gating:** Multiply the input by a trainable weight matrix $W_{g}$ and then apply the $softmax$ function: $$G_{\sigma}(x) = softmax(x \cdot W_{g})$$
- **Noisy Top-K Gating:** Add two components: sparsity and noise
	- Add tunable Gaussian noise, then keep only the top $k$ values, setting the rest to $-\infty$. $$G(x) = softmax(KeepTopK(H(x), k))$$ $$H(x)_{i}= (x \cdot W_{g})_{i} + StandardNormal() \cdot Softplus((x \cdot W_{noise})_{i})$$ $$KeepTopK(v, k)_{i}= \begin{cases}v_{i} & \text{if } v_{i} \text{ is in the top } k \text{ elements of }v. \\ -\infty & \text{otherwise}.\end{cases}$$
		- Sparsity save computation.
		- Noise term helps with load balancing. The amount of noise per component is controlled by trainable matrix $W_{noise}$ .
- **Training:** By simple back-propogation.

# Addressing Performance Challenges
### Shrinking Batch

- If the gating network chooses $k$ out of $n$ experts for each example, then for a batch of $b$ examples, each expert receives a much smaller batch of approximately $\frac{kb}{n} << b$ examples.
	- Making the original batch size as large as possible => limited by the memory.
- **Mixing Data Parallelism and Model Parallelism:** 
	- Method: (Link)
	- If the model is distributed over $d$ devices, and each device processes a batch of size $b$, each expert receives a batch of approximately $kbd/n$ examples
	- Hierarchical MoE: 
		- Primary gating network employs data parallelism.
		- Secondary MoEs employ model parallelism.
- **Taking Advantage of Convolutionality:**
- **Increasing Batch Size for a Recurrent MoE**:
### Network Bandwidth

- The ratio of computational to the size of its input and output must exceed the ratio of computational to network capacity of the computing device.
# Balancing Expert Utilization

- Gating network tends to converge to a state where it always produces large weights for the same few experts.
- Soft constraint approach:
	- Define the importance of an expert relative to a batch of training examples: 
	$$Importance(X) = \sum\limits_{x\in X} G(x).$$
	- Define an additional loss $L_importance$, which is added to the overall loss function for the model: 
	$$L_{importance}(X) = w_{importance} \cdot CV(Importance(X))^2 $$
		- square of the coefficient of variation of the set of important values, multiplied by a hand-tuned scaling factor $w_{importance}$.
- Experts may still receive very different numbers of examples. To solve this, a second loss function is introduced $L_{load}$, which ensures balanced loads.
# Experiments

- **1 Billion Word Language Modeling Benchmark:**
    
    - Researchers trained various MoE models with roughly equal computational costs to baseline models without MoEs. They varied the number of experts (both flat and hierarchical MoEs) while keeping the operations per timestep similar.
    - **Superiority:** Increasing model capacity by increasing the number of experts in the MoE layer led to **significantly lower perplexity** on the test set compared to computationally-matched baseline models with similar parameter counts but no sparse conditional computation. For example, a model with **4096 experts achieved a 24% lower perplexity**.
    - They also trained high-capacity MoE models (around 4 billion parameters) with varying computational budgets.
    - **Superiority:** Even the fastest of these high-capacity MoE models **outperformed the best previously published result** on this benchmark (by Jozefowicz et al., 2016) after 10 epochs, despite requiring only **6% of the computation**. The models with larger computational budgets achieved even lower perplexity. This demonstrates that MoEs can achieve better results with significantly less computational cost and training time.
- **100 Billion Word Google News Corpus:**
    
    - To test scalability with larger datasets and capacities, models were trained on a 100 billion word corpus. The number of experts varied up to **131,072**, resulting in a model with **137 billion parameters** in the MoE layer.
    - **Superiority:** Training over the full 100 billion words showed significant improvements in test perplexity as the number of experts (and thus model capacity) increased, up to **65,536 experts (68 billion parameters)**. This model achieved a **39% lower perplexity** than a computationally matched baseline LSTM model. This highlights the ability of MoEs to effectively utilise vast amounts of training data by scaling model capacity without a proportional increase in computation.
- **Machine Translation (Single Language Pair):**
    
    - MoE layers were applied to a modified version of the GNMT architecture for English to French (En→Fr) and English to German (En→De) translation tasks. MoE layers were inserted in both the encoder and decoder.
    - **Superiority:** The MoE-augmented models achieved **significantly higher BLEU scores** on the WMT’14 En→Fr and En→De benchmarks compared to strong GNMT baselines (Wu et al., 2016) without using reinforcement learning refinement. For En→Fr, a **1.34 BLEU score improvement** was achieved, and for En→De, a **1.12 BLEU score improvement**. Perplexity scores were also better. On a Google Production En→Fr dataset, their model achieved a **1.01 higher test BLEU score** with considerably less training time. These results demonstrate the effectiveness of MoEs in improving translation quality.
- **Multilingual Machine Translation:**
    
    - A single MoE-augmented model was trained on a combined dataset of twelve language pairs, following the setup of Johnson et al. (2016).
    - **Superiority:** The multilingual MoE model achieved **19% lower perplexity** on the development set than a multilingual GNMT model. More importantly, it **significantly outperformed the multilingual GNMT model on BLEU score for 11 out of the 12 language pairs** (by as much as 5.84 points) and even surpassed the performance of separately trained monolingual GNMT models on 8 of the 12 language pairs. This showcases the ability of MoE models to effectively learn and share knowledge across multiple languages due to their increased capacity.

In summary, the experiments consistently demonstrate that the introduction of the **Sparsely-Gated Mixture-of-Experts layer** leads to **substantial improvements in model performance** across different natural language processing tasks. These improvements are evident in the form of **lower perplexity in language modelling and higher BLEU scores in machine translation**. Furthermore, the MoE models often achieve these superior results with **greater parameter efficiency** and sometimes even at a **lower computational cost** compared to traditional dense neural networks. The **scalability** of the MoE approach to extremely large models and datasets further underscores its potential for advancing the state-of-the-art in deep learning.

# Appendices

### Appendix A: Load-Balancing Loss

- Smooth estimator $Load(X)$ of the number of examples assigned to each expert for a batch $X$ of inputs $\implies$ allows back-propagate gradients.
- Define $P(x,i)$ as the probability that $G(x)_i$ is nonzero, given a new random choice of noise on element $i$, but keeping the already-sampled choices of noise on the other elements.
	- $G(x)_i$ is nonzero $\iff$ $H(x)_{i} >$ the $k^{th}$-greates element of $H(x)$ excluding itself.
	- $kth\_excluding(v, k, i)$ means the $k^{th}$ highest component of $v$, excluding component $i$.
$$P(x, i) = Pr\Bigg((x \cdot W_{g})_{i} + StandardNormal() \cdot Softplus((x \cdot W_{noise})_{i}) > kth\_{excluding}(H(x), k, i)  \Bigg)$$
- Simplifying, we get: 
$$P(x, i) = \Phi \Bigg( \frac{(x \cdot W_{g})_{i} - kth\_{excluding}(H(x), k, i)}{Softplus((x \cdot W_{noise})_{i})} \Bigg)$$ where $\Phi$ is the CDF of the standard normal distribution.
$$Load(X) = \sum\limits_{x \in X} P(x, i)$$
- The load loss: 
$$L_{load}(X) = w_{load}\cdot CV(Load(X))^2$$
- **Initial Load Imbalance:** Initialize the matrices $W_g$ and $W_{noise}$ to all zeros.
### Appendix B: Hierarchical Mixture of Experts

- A primary gating network chooses a sparse weighted combination of "experts", each of which is itself a secondary mixture-of-experts with its own gating network.
- If the hierarchical MoE consists of $a$ groups of $b$ experts each, the output of the MoE is given by: 
$$y_{H}= \sum\limits_{i=1}^{a}\sum\limits_{j=1}^{b}G_{primary}(x)_{i}\cdot G_i(x)_{j}\cdot E_{i,j}(x)$$
- Our metrics of expert utilization change to the following: 
$$Importance_{H}(X)_{i,j}= \sum\limits_{x \in X} G_{primary}(x)_{i}\cdot G_{i}(x)_{j}$$ 
$$Load_H(X)_{i,j}= \frac{Load_{primary}(X)_{i} \cdot Load_{i}(X^{(i)})_{j}}{|X^{(i)}|}$$
### Appendix C, D, E: Experiment Details

### Appendix F: Strictly Balanced Gating

- The models ran faster if every expert received exactly the same batch size.
- The softmax gating function: 
$$G_{\sigma}(x) = softmax(x \cdot W_{g})$$
- **Sparse Gating (alternate formulation):** 
	- The mask $M(G_{\sigma}(x))$ specifies which experts are assigned to each input example: 
	$$G(x)_{i}= \frac{G_{\sigma}(x)_{i}M(G_{\sigma}(x))_i}{\sum\limits_{j=1}^{n}G_{\sigma}(x)_{j}M(G_{\sigma}(x))_j}$$
- **Top-K Mask:**
	- Let $M(v) = TopK(v, k)$, where: 
	$$TopK(v, k)_{i}= \begin{cases}1 & \text{if } v_{i} \text{ is in the top } k \text{ elements of }v. \\ 0 & \text{otherwise.}\end{cases}$$
- **Batchwise Mask:** 
	- An alternative mask function operates over batches of input vectors. It keeps the top $m$ vales per expert across the training batch, where $m = \frac{k|X|}{n}$, so that each example is sent to an average of $k$ experts: 
	$$M_{batchwise} (X, m)_{j,i} = \begin{cases}1 & \text{if } X_{j,i} \text{ is in the top } m \text{ values for to expert }i. \\ 0 & \text{otherwise.}\end{cases}$$
	- This requires modifications to the inference when not have a large batch of examples. The following mask is used at inference time: 
	$$M_{threshold} (x, T)_{i} = \begin{cases}1 & \text{if } x_{i} > T_{i}. \\ 0 & \text{otherwise.}\end{cases}$$
	- To learn the threshold values, an additional loss is applied which is minimized when $M_{batchwise} \approx M_{threshold}$: 
	$$L_{batchwise}(X, T, m) = \sum\limits_{j=1}^{|X|}\sum\limits_{i=1}^{n}(M_{threshold}(x, T)_{i}- M_{batchwise}(x, m)_{j,i})(X_{j,i}- T_i)$$
### Appendix G: Attention Function