---
{"up":["[[Machine Learning MOC]]"],"related":null,"created":"2024-10-15T21:21:17","tags":["quant","machine_learning"],"dg-publish":true,"permalink":"/research-labs/notes/feature-selection-and-extraction-techniques-for-stock-market-prediction/","dgPassFrontmatter":true}
---


>[!Abstract] Research questions
>This survey aimed to answer the following research questions:
>- Which types of feature selection and extraction techniques are applied in stock market prediction?
>- Which structured inputs are widely used in prediction models?
>- How can a feature learning process improve prediction accuracy?
# Introduction
- Data inputs and prediction outputs:
	- *Basic features*: stock value as OHLCV data
	- *Technical indictors*: RSI, stochastic oscillator, MACD, etc.
	- *Fundamental indicators*: economic indicators ranging from macroeconomic factors to microeconomic factors.
- Dimensionality reduction approaches *(kỹ thuật giảm chiều)*
	- **Feature selection**: maintain subset of original features
	- **Feature extraction**: creates new features from original dataset
# Feature selection
## Filter methods
- **Filter methods** xếp hạng các feature dựa trên mức độ liên quan của chúng với các thuật toán ML. They act as a preprocessing step by selecting highly ranked features and applying them to ML methods.
	- Therefore, they are computationally fast and robust to overfitting, but they don't consider the dependency between features.
	- Filter methods use statistical performance measures such as the correlation/distance between features and output variables.
- **Correlation**: là cách đơn giản nhất để tính điểm tương quan phù hợp giữa *feature* và *target variable*
	- Có nhiều loại *correlation*: Pearson correlation, Kendall rank correlation, Spearman correlation, Point-Biserial correlation.
	- Tuy nhiên hãy cẩn thận khi sử dụng *correlation*. Bởi vì correlation không có nghĩa là có mối quan hệ nhân quả với nhau, đôi khi chúng ta còn sẽ gặp phải tương quan giả *(spurious correlation)*. Và correlation thấp không có nghĩa là *no dependency*.
	- Anscombe's quartet là 1 nhóm các tập dữ liệu $(x,y)$ có cùng *mean, standard deviation và regression line*, nhưng khác hoàn toàn nhau về bản chất. Nó thường được sử dụng để minh hoạ tầm quan trọng của việc quan sát các tập dữ liệu thông qua các biểu đồ thay vì chỉ dựa trên các thống kê cơ bản. ![|800](https://i.imgur.com/wNHO0wH.png)
- **Relief algorithm**: is used for feature selection in regression and classification problems. Thuật toán này sẽ tính toán *importance score* cho từng *feature* dựa trên mức độ mà *feature* đó có thể phân biệt giữa các trường hợp lân cận gần nhất. It returns một danh sách các *feature* được xếp hạng hay các *feature* có điểm số cao nhất dựa trên một ngưỡng nhất định
## Wrapper methods
- In wrapper methods, *feature selection* được *wrapped* trong *learning process* của thuật toán ML. Do đó, các method này tìm kiếm một tập hợp con các feature cung cấp *hiệu suất dự đoán cao nhất*. Họ cũng dựa vào performance của predictor để có được *optimal feature subset* và sử dụng *accuracy* của predictor làm *objective function*.
- **Recursive feature elimination (RFE)** là 1 *wrapper-type feature selection* nổi tiếng bao gồm một quy trình lặp để huấn luyện mô hình ML. RFE tính toán tiêu chí xếp hạng tất cả *feature* trong mỗi lần huấn luyện và loại bỏ các *feature* có *importance score* thấp nhất, sau đó *train model* on the basis of the *new feature set.*
## Embedded methods
- *Embedded methods* combine các đặc tính của *filter method* và *wrapper method* cùng với *form feature selection* như 1 phần của *training process* bằng cách tích hợp cả *algorithm modeling* và *feature selection*.
- Do đó, chúng hiệu quả hơn về mặt tính toasn và tránh được overfitting so với *wrapper metod*.
- *Embedded methods* và *wrapper methods* được coi là *subset evaluation techniques* có thể nắm bắt được sự phụ thuộc và tương tác giữa các features. Khả năng này làm cho các methods này vượt trội hơn các *filter methods*
### Random forest
- **Random forest** là *ensemble learning method* được sử dụng cho classification và regression problems. Gần đây, RF ngày càng được sử dụng nhiều như là một *feature selection method* vì nó có nhiều ưu điểm, chẳng hạn như *international estimaté of error*, *correlations*, và *feature importance scores*.
- RF cung cấp 2 *methods* cho việc tính toán *feature importance scores*:
	- **Mean decrease accuracy (MDA)**: Mức độ chính xác của dự đoán mà mô hình mất đi sau khi loại bỏ từng feature.
	- **Mean decrease impurity (MDI)**: Mức độ đóng góp của từng feature vào *homogeneity* của các *nodes* và *leaves* với từng *decision-tree model*.
## Information theory-based methods
- *Information theory-based methods* sử dụng *mutual information(MI)*  để đạt được *importance score* của từng feature: $$MI(A, B)=\sum_{a,b}p(a,b) \cdot \log{\frac{p(a,b)}{p(a)p(b)}}$$
- Định nghĩa này liên quan đến *Kullback-leibler (KL) divergence* between two distributions. *KL divergence* đo lường sự phụ thuộc của 2 phân phối. In feature selection, choose features that *minimize* $MI(A,B)$ để đảm bảo chúng không liên quan đến nhau.
- Information theoretic algorithms *assign score* to each feature based on *mức độ liên quan đến target variable* và *mức độ redundant của feature này với các feature khác đã được chọn cho đến nay.* Các feature được chọn lần lượt cho đến khi đủ số feature mong muốn.
```pseudo
# Algorithm 1: Information theoretic algorithm
Data: all features, target data, desired number of features n 
Result: selected features 
for i ← 0 to n do  
	for each feature not selected so far do  
	Calculate relevance i.e mutual information with the target variables (A) 
	Calculate mutual information with each of the features already selected. 
	Take the average of values from the previous step (B) 
	Assign score S = A - B 
	end  
	Select the feature with the highest score and add to the selected list of features. 
end
```

# Feature extraction
## Principal component analysis (PCA)
- **Principal component analysis (PCA)**, là một *statistical-based feature extraction method*, là một kỹ thuật phổ biến cho *dimensionality reduction*. It *transform* a *high-dimensional feature vector* into a *low-dimensional feature vector* with *uncorrelated components* by calculating *eigenvectors of covariance matrix of original features*. 
## Autoencoder
- *A neural network-based unsupervised learning model called the autoencoder (AE)* reconstructs inputs to *neural network* in output layer.
	- The *encoder* reduces the input to codeword-sized dimension,
	- The *decoder* uses codeword to *reassemble* original input data.
![](https://i.imgur.com/Nw2Zomz.png)
