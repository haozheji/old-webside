---
layout: post
title: Courant-Fischer 定理的证明
---
\\( A \\)为\\( n \\)阶实对称矩阵，有特征值\\[ \lambda_1\ge \lambda_2\ge\cdots\ge\lambda_n \\]则有：
\\[ \min_{\dim V=n-k+1}\max_{0\ne v\in V}\frac{v^HAv}{v^Hv}=\lambda_k \\]
该定理又被称为极小-极大定理.

<!--more-->

它的对偶问题，也就是极大-极小定理，表述如下：
\\[ \max_{\dim V=k}\min_{0\ne v\in V}\frac{v^HAv}{v^Hv}=\lambda_k \\]

\\( proof: \\)
令\\[ \mu(V)=\max_{0\ne v\in V}\frac{v^HAv}{v^Hv} \\]
且对应\\( \lambda_1,\lambda_2,\cdots,\lambda_n \\)的特征向量为\\( q_1,q_2,\cdots,q_n\\).

考虑\\( n-k+1 \\)维子空间\\( V_0 \\).
\\[ V_0\perp V^*=span\left\\{ q_1,q_2,\cdots,q_{k-1} \right\\} \\]
因为\\(n \\)阶实对称矩阵的特征向量为\\( Re^n \\)的一组标准正交基。因此

\\(V_0=(V^*)^{\perp}=span\left\\{q_k,q_{k+1},\cdots,q_n\right\\}\\)

即对任意\\(v\in V_0\\),存在\\(\left\\{c_i\right\\}_{i=k}^n\\)使得：

\\[ v=c_k q_k+c_{k+1}q_{k+1}+\cdots+c_{n}q_n \\]
则有：
\\[\mu(V_0)=\max_{c_k,\cdots,c_n}\frac{\sum_{i=k}^n\lambda_ic_i^2}{\sum_{i=k}^{n}c_i^2}=\lambda_k\\]
考虑任意\\( \dim{V'}=n-k+1\\)且\\(V'\ne V_0 \\).直观上认识，\\(V'\\)可能包含原有\\(V_0\\)的成分也可能不包含(换句话说就是\\(V'\\)在\\(V_0\\)上投影的子空间可以有分量，也可以为\\(\{0\}\\).但\\(V'\\)在\\(V_0\\)的正交子空间\\(V^*\\)中一定是有投影分量的。

这时我们把\\(V'\\)写成两个正交子空间的直和的形式，一部分是在\\(V_0\\)中的投影(可能为\\(\{0\}\\))，另一部分是在\\( V^* \\)中的投影。
后者一定是存在分量的,且一定可以用\\( V^* \\)的一部分基(假设\\(j\\)个)张成，因为它是\\(V^*\\)的子空间。
则存在\\(q_{i_1},q_{i_2},\cdots,q_{i_j},(1\le j\le k-1,1\le i_1,i_2,\cdots,i_j\le k-1)\\) 使得任意\\(v'\in V'\\)
\\[ v'=\sum_{l=1}^jc_{i_l}q_{i_l}+v_x\\] 
\\[v_x\in V'|span\left\\{ q_{i_1},\cdots,q_{i_j}\right\\} \\]
\\(v_x\\)分量为\\(v'\\)在\\(V_0\\)中的投影，故为\\(q_k,\cdots,q_n\\)的线性组合(系数可以为0).
而同时\\(v'\\)还含有分量\\[q_{i_1},q_{i_2},\cdots,q_{i_j},(1\le j\le k-1,1\le i_1,i_2,\cdots,i_j\le k-1)\\]它们对应更大的特征值。即\\(v'\\)可以写成：
\\[ v'=c_{i_1}q_{i_1}+\cdots+c_{i_j}q_{i_j}+b_kq_k+\cdots+b_nq_n\\]
则有：
\\[ \mu(V')=\max_{c,b}\frac{\lambda_{i_1}c_{i_1}^2+\cdots+\lambda_{i_j}c_{i_j}^2+\lambda_kb_k^2\cdots+\lambda_nb_n^2}{c_{i_1}^2+\cdots+c_{i_j}^2+b_k^2\cdots+b_n^2}=\max_{1\le l\le j}\lambda_{i_l}>\lambda_k \\]
即
\\[ \min_{\dim V=n-k+1}\mu(V)=\lambda_k \\]
当且仅当\\(V=V_0\\)时取到.

作为特征分析中有较多应用的定理，对于它的证明却极其罕至。其中笔者认为写得比较详细精彩的是来自于台湾国立交通大学的周志成老师的一篇博文<a href="https://ccjou.wordpress.com/2010/03/16/hermitian-%E7%9F%A9%E9%99%A3%E7%89%B9%E5%BE%B5%E5%80%BC%E7%9A%84%E8%AE%8A%E5%8C%96%E7%95%8C%E5%AE%9A/">Hermitian 矩陣特徵值的變化界定</a>.从特征向量和子空间的本质出发，步步深入，应该说讲的十分透彻了。除此之外清华大学张贤达老师的《矩阵分析与应用》一书中也有该定理的证明;可能由于篇幅所限，证明过程有所压缩，笔者觉得理解起来不太容易。

参考了以上的证明，笔者决定从自己理解的角度给出证明。从特殊情况推广到一般，建立之间的桥梁应该是主要思路;这一定理也给出Rayleigh商的直观，我认为是二次型对应的闭超曲面(超椭球？姑且这么叫)的最长轴长在不同子空间的取值。如何将对于定理的直观转化为严密的数学文字需要再三斟酌，或许这就是线性代数的魅力吧。

