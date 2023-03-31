---
title: What is BLAS?
subtitle: notes on Basic Linear Algebra Subprograms
layout: default
date: 2023-03-30
keywords: computer science, mathematics
summary: notes on Basic Linear Algebra Subprograms
published: true
---

#### tags: `computer science`, `mathematics`


Basic Linear Algebra Subprograms(BLAS) is a set of low-level routines for linear algebra operations. Most of the numerical libraries like NumPy and R do their linear algebra computations based on these standard operations. BLAS is often optimized for specific hardware for better performance; thus, BLAS has numerous different implementations depending on the vendor or type of processing unit(CPU/GPU).

Operations in BLAS are categorized into three levels based on their complexity.

### Level 1: Vector operations
$O(n)$ operations on $O(n)$ operands

ex)  `axpy`, "a x plus y"
{% katexmm %}
$$
y \leftarrow \alpha x + y
$$
{% endkatexmm %}

where $x, y \in \mathbb{R}^n$ and $\alpha \in \mathbb{R}$.
$x, y$ are $n$-dimensional vectors each, hence we have $2n$ numbers. $\alpha$ is a scalar, hence we have $2n + 1$ numbers in total.
{% katexmm %}
$$
y_i = \alpha \times x_i + y_i \quad \text{for }i = 1, ..., n
$$
{% endkatexmm %}
We have two floating point operations($1$ multiply and $1$ add) for each $i$ and we have to repeat it for $n$ times, thus we have $2n$ floating point operations in total. 

In summary,  
$2n + 1$ numbers $\rightarrow O(n)$ operands  
$2n$ floating point operations $\rightarrow O(n)$ operations  

### Level 2: Matrix-vector operations
$O(n^2)$ operations on $O(n^2)$ operands

ex) `gemv`, "generalized matrix-vector multiplication"
{% katexmm %}
$$
y \leftarrow \alpha A x + \beta y
$$
{% endkatexmm %}
where $A \in \mathbb{R}^{n \times n}$, $x, y \in \mathbb{R}^n$ and $\alpha,\beta \in \mathbb{R}$.

{% katexmm %}
$$
y_i = \alpha \times \sum_{j} A_{ij}\times x_j + \beta \times y_i  \quad
\text{for }i = 1, ..., n
$$
{% endkatexmm %}

Here, $A$ has $n^2$ numbers, $x, y$ has $n$ numbers each, thus we have $n^2 + 2n + 2$ numbers.  
For each $i$, we have $n+2$ multiplies and $(n-1) + 1$ adds, hence $n(2n+2) = 2n^2 + 2n$ FP_OPs.

In summary,  
$n^2 + 2n + 2$ numbers $\rightarrow O(n^2)$ operands  
$2n^2 + 2n$ floating point operations $\rightarrow O(n^2)$ operations  

### Level 3 Matrix-matrix operations
$O(n^3)$ operations on $O(n^2)$ operands

ex) `gemm`, "generalized matrix multiplication"
{% katexmm %}
$$
C \leftarrow \alpha AB + \beta C
$$
{% endkatexmm %}

where $A,B,C \in \mathbb{R}^{n \times n}$, and $\alpha,\beta \in \mathbb{R}$.

{% katexmm %}
$$
C_{ij} = \alpha \times \sum_{k} A_{ik}\times B_{kj} + \beta \times C_{ij}  \quad
\text{for }i,j = 1, ..., n
$$
{% endkatexmm %}
Here, $A,B,C$ has $n^2$ numbers each, thus we have $3n^2+2$ numbers.  
For each $i$ and $j$, we have $n+2$ multiplies and $(n-1) + 1$ adds, hence $n^2(2n+2) = 2n^3+2n^2$ FP_OPs.

In summary,  
$3n^2 + 2$ numbers $\rightarrow O(n^2)$ operands  
$2n^3 + 2n^2$ floating point operations $\rightarrow O(n^3)$ operations