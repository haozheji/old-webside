---
layout: post
title: positive matrix
---

{% raw %}

Property of positive matrix \\(A\\)

<!--more-->

(1) The spectral radius \\(\rho (A)\\) is an eigenvalue of A; the geometric and algebraic multiplicity is 1. (Let \\(\sigma(A)\\) be the set consisted of \\(A\\)'s eigenvalues, then \\(\rho(A) = \max_{\lambda\in\sigma(A)}\|\lambda\|\\).)

(2) The eigenvector \\(x\\) associated with the eigenvalue \\(\rho (A)\\) can be taken to have nonnegative entries; other eigenvectors cannot be taken to have nonnegative entries!

(3) If every entry of \\(A\\) is positive, then \\(\rho(A)\\) is a simple eigenvalue, that is strictly larger than the modulus of any other eigenvalues.

(4) If every entry of \\(A\\) is positive, then \\(\lim_{m\to\infty}(\frac{A}{\rho(A)})^m\\) exists and is a rank-one matrix; each of whose columns is proportional to the eigenvector x.



*Corollary*

Let \\(x\\) be \\(A\\)'s P-F vector, i.e. \\(Ax=\rho(A)x\\). \\(y\\) be its left P-F vector, i.e.\\(y^TA=\rho(A)y^T\\), and they normalized to 1, i.e. \\(x^Ty=1\\). Then 

\\[\lim_{m\to\infty}(\frac{A}{\rho(A)})^m=xy^T\\] 

proof:

Exist \\(S=(x, S'), (S^{-1})^T=(y, Z')\\), such that 

$$
(\frac{A}{\rho(A)})^m =S
\begin{pmatrix}
1&0\\
0&(\rho(A)^{-1}B)^m
\end{pmatrix}
S^{-1}\\
\to(x, S')
\begin{pmatrix}
1&0\\
0&0_{n-1}
\end{pmatrix}
\begin{pmatrix}
y^T\\Z'^T
\end{pmatrix}=xy^T , \quad m\to \infty
$$

(5) There is a unique vector \\(x=[x_i]\in C^n\\) such that \\(Ax=\rho(A)x \\) and \\(\sum_ix_i=1\\). Such a vector must be positive.

# Nonnegative matrix

properties:

(1) Let \\(A, B \in M_n\\) and suppose that B is nonnegative. If \\(\|A\|\le B\\) (the absolute, not determinant), then \\(\rho(A)\le\rho(\|A\|)\le \rho(B)\\).

(2) Let \\(A=[a_{ij}]\in M_n\\) br nonnegative. Then 


$$
\min_{1\le i\le n}\sum_{j=1}^na_{ij}\le\rho(A)\le\max_{1\le i\le n}\sum_{j=1}^{n}a_{ij}
$$


The spectral radius of \\(A\\) is bounded by the minimum row sum and the maximum row sum. Similarly, \\(\rho(A)\\) is bounded by the minimum column sum and maximum column sum.

proof:

The definition of the matrix norm is given by:

$$
\|A\|_p=\max_{\|x\|_p=1}\|Ax\|_p, \quad \|x\|_p=(\sum_{i=1}^nx_i^p)^{1/p}
$$

The general norm is given by Cauchy-Schwartz theorem. 

$$
\|A\|\cdot \|x\|\ge \|Ax\|, \quad
\|A\|\ge\frac{\|Ax\|}{\|x\|}
$$

Specifically, we have:

$$
\|A\|_1=\max_{1\le j\le n}\sum_{i=1}^n|a_{ij}|\\
\|A\|_{\infty}=\max_{1\le i\le n}\sum_{i=1}^n|a_{ij}|\\
$$

Lemma: The eigenvalues of matrix A is no larger than the matrix norm, i.e. \\(\|\lambda\|\le\\|A\\|\\)

$$
Ax=\lambda x\\
|\lambda|\cdot\|x\|=\|Ax\|\le\|A\|\cdot\|x\|\\
$$

The left inequality can be demonstrated this way.

Let \\(\alpha=\min_{1\le i\le n}\sum_{j=1}^na_{ij}\\). Define \\(B=[b_{ij}]\\), and \\(b_{ij}=\alpha a_{ij}(\sum_{k=1}^na_{ik})^{-1}\\). Then \\(A\ge B\ge 0\\), i.e. \\(\rho(A)\ge \rho(B)\\) and \\(\sum_{j=1}^nb_{ij}=\alpha\\) for all \\(i=1,\cdots,n\\), i.e. \\(\rho(B)=\alpha\\). Therefore, 


$$
\min_{1\le i\le n}\sum_{j=1}^na_{ij}\le\rho(A)
$$

(3) If \\(A\in M_n\\) is nonnegative, for nonnegative \\(x\\):


$$
\rho(A)=\max_{x\ge 0}\min_{1\le i\le n}\frac{(Ax)_i}{x_i}
$$

proof:

From (2), 
$$
\rho(A)\ge \min_{1\le u\le n}(Ax)_i/x_i.
$$
The maximum can be obtained when \\(x\\) satisfies \\(Ax=\rho(A)x\\)

(4) Suppose there is a positive vector \\(x\\) and a nonnegative real number \\(\lambda\\) such that either \\(Ax=\lambda x\\) or \\(x^TA=\lambda x^T\\). Then \\(\lambda = \rho(A)\\).

proof: 

Suppose x is the corresponding eigenvector of \\(\lambda\\), y is the left eigenvector of \\(\rho(A)\\), then. 

$$
Ax=\lambda x, \quad y^TA=\rho(A)y^T\\
\rho(A)y^Tx=y^TAx=\lambda y^Tx\\Thus\quad \rho(A)=\lambda.
$$
{% endraw %}
