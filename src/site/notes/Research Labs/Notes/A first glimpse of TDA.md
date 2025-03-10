---
{"up":["[[Topological Data Analysis]]"],"related":"[[Quantum topological data analysis for detecting financial crashes]]","created":"2025-03-07 11:29:42","tags":["#topology"],"dg-publish":true,"permalink":"/research-labs/notes/a-first-glimpse-of-tda/","dgPassFrontmatter":true}
---

# What is topological data analysis?
## Topology and Homology
Topology nghiên cứu các tính chất của *geometry objects* mà không bị ảnh hưởng bởi các *continuous deformation*, such as stretching, twisting, crumpling, and bending.

Homology serves as a tool to study and quantify the *topological properties of spaces*. Homology of an object thường được tóm gọn thông qua *$k$-th Bettin numbers*, which count the *number of $k$-dimensional holes* withing object.
- $\beta_0$: Number of *connected components* (số đỉnh riêng biệt)
- $\beta_1$: Number of *loops* (lỗ 1 chiều)
- $\beta_2$: Number of *enclosed volumes* (lỗ 2 chiều)
Những con số này cung cấp 1 *signature* về cấu trúc hình học của dữ liệu

## Simplicial complex
In finance, input data is typically represented as time series, sau đó được *transform* into a *series of discrete points*. To model the underlying structure with them, we construct **simplicial complex** (specifically, Vietoris-Rips complex), **collection of simple shapes that connect the points together**.

Those simple shapes arre caller *simplex* (đơn hình - hiểu đơn giản là phiên bản tổng quát của tam giác hay tứ diện ở nhiều chiều hơn). *$k$-simplex* is collection of $k+1$ đỉnh with $\frac{k(k+1)}{2}$ edge in $k$ dimensions.  

Chúng ta chọn 1 ngưỡng khoảng cách $\epsilon$; nếu 2 điểm bất kỳ cách nhau < $\epsilon$, chúng sẽ được nối bằng một đoạn thẳng trong simplicial complex. As *$\epsilon$ increases*, more connections are added, and *lower-order components* may *merge* into *higher-order components* (decrease lower-order Betti numbers and increase in higher-order Betti numbers). The study of how *topological properties change across sequence of resolution threholds* is called **persistent homology**.

>[!Example]
>![|800](https://i.imgur.com/rWO60VB.png)
>When $\epsilon$ is small, no lines connect the points. Consequently, $\beta_0=5$, as there are five discrete points, each representing an independent connected component, and no higher-dimensional features are present. 
>
>As $\epsilon$ increases, Betti numbers for configuration on the right become:
>- $\beta_0=2$: Two connected components (a line segment and a triangle)
>- $\beta_1=1$: One 1-dimensional hole (triangle encloses a region)
>- $\beta_k=0$ for $k>2$: No higher-dimensional exist.

