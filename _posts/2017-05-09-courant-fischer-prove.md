---
layout: post
title: Courant Fischer定理的证明
mathjax: true
categories: Math
tags: [linear algebra]
---

对$n$阶实对称矩阵$A$有特征值$\lambda_1\le \lambda_2\le \cdots\le \lambda_{n}$，对应特征向量$x_1,x_2,\cdots ,x_n$，则对任意$k$维子空间$V_k$，有：

\[
\lambda_{n-k+1}=\max_{V_k}\min_{x\in V_k}\frac{x^TAx}{x^Tx}
\]

<!-- more -->

这个定理得到在不同约束下的*Rayleigh*商的极值。笔者最欣赏的证明出自于 [Gilbert Strang ](http://www-math.mit.edu/~gs/)的 *Linear Algebra and Its Application*，循序渐进由浅入深，为读者展现了解决问题的思考过程，读来颇有收获。在此整理一下，附上一些自己的理解。


<div align="center">
<img src="/img/cupcakematrix.jpg" alt="cupcake matrix"  />
<p>Gilbert Strang and his favourite -1, 2, -1 matrix</p>
</div>


### *Lemma 1* 

*Rayleigh's Principle:*

\[
\lambda_1\le R(x)=\frac{x^TAx}{x^Tx}\le \lambda_n
\]

当$x=x_1$时取到最小值；当$x=x_n$时取到最大值。

*proof:*

先从几何上理解一下Rayleigh商的含义，以最小化$R(x)$为例。令分子等于1得到$n$维超椭球的方程，这时候问题转变为最大化分母$x^Tx=\|\|x\|\|^2$。也就是找到一个方向（轴）使得在这个方向上超椭球面上的点到原点的距离最大（最长轴）。显然，沿着最长主轴(major axis)的方向就能得到$R(x)$的最小值，这个方向也很好通过$A$的相似对角化确定。

\[
R(x)=\frac{(Qy)^TA(Qy)}{(Qy)^T(Qy)}=\frac{y^T\Lambda y}{y^Ty}=\frac{\lambda_1y_1^2+\cdots +\lambda_ny_n^2}{y_1^2+\cdots +y_n^2}
\]

$Q$为正交阵，等价于进行有限次旋转和镜射，可以理解为将$x$在自然基下的坐标换到了$A$的特征向量基下。（注意上式中$y_i$表示坐标）由分子可以看出超椭球的主轴长度反比于$\frac{1}{\sqrt \lambda}$, 因此最长主轴方向就是$x_1$的方向，在$A$ 特征向量的基下坐标为$y_1=1,y_2=0,\cdots ,y_n=0$.也可以利用不等式：

\[
\lambda_1(y_1^2+\cdots +y_n^2)\le \lambda_1y_1^2+\cdots\lambda_ny_n^2
\]

类似地可以求出在$x_n$方向上，$R(x)$取到极大值。实际上除了边界的特征向量为极值点, 中间的特征向量则是$R(x)$的鞍点(saddle points)。一个典型的鞍点：

<div align="center">

<img src="/img/z=x^2-y^2.png" alt="z=x^2-y^2" style="zoom:70%"/>

<p>saddle point of z=x^2-y^2</p>

</div>

鞍点的困难在于,对于一个特定的$x$,我们不知道$R(x)$和那些中间的特征值$\lambda_2,\cdots, \lambda_n$的大小关系. 比如说我们想要让$R(x)$的最小值取到第$j$个特征值, 利用实对称矩阵的特征向量$x_i$相互正交的性质, 直接的想法是约束变量$x$取到与$x_1,\cdots,x_{j-1}$正交, 即$x$取值于子空间$span\\{x_j,\cdots,x_n\\}$. 这样$R(x)$表达式中的$y_1=\cdots=y_{j-1}=0$, Rayleigh 商也化为:

\[
\frac{\lambda_{j}y_j^2+\cdots+\lambda_ny_n^2}{y_j^2+\cdots+y_n^2}
\]

上式取到当\(y_j=1\)时取到最小值\(\lambda_j\).总结成引理二.

### *Lemma 2*

\[\lambda_j=\min R(x), \quad given\quad x^Tx_1=\cdots=x^Tx_{j-1}=0\]

大部分时候\(A\)的特征向量是未知的, 也就是上述引理的约束不知道. 比如说我们考虑在不知道\(x_1\)的情况下得到\(R(x)\)和\(\lambda_2\)的关系. 这时我们使用任意一个向量\(z\)来代替\(x_1\). 当它们相等时, \(R(x)\)就能取到最小值\(\lambda_2\), 事实上就算在它们不相等的情况下, 我们可以得到:

\[\lambda_2 = \max_z \min_{x^Tz=0}R(x)\]

或用\(z\)的正交补\(V_{n-1}\)写作:

\[\lambda_2= \max_{V_{n-1}} \min_{x \in V_{n-1}}R(x)\]

*proof:*

任意给定\(z\), 存在\(\alpha, \beta\neq 0\) 使得\(x=\alpha x_1+\beta x_2\)与\(z\)正交. 一定存在这样的\(\alpha, \beta\)的原因是, 正交条件只给这两个变量施加了一个约束, 它们还保留一个自由度. 对任意满足该条件的组合:

\[R(x)=\frac{\lambda_1 \alpha^2+\lambda_2 \beta^2}{\alpha^2+\beta^2}\le \lambda_2\]

将上述定理推广, 即可得到*Courant Fischer*定理, 下面给出证明.

*proof:*

对任意子空间\(V_{k}\in \Re^n\), 取\\(x \in V_{k}\). 考虑\(V_{k}\)的正交补\(W_{n-k}\), 取定\(W_{n-k}\)的一组基\(w_1,\cdots, w_{n-k}\), \(x\)应满足分别垂直于这\(n-k\)个向量, 相当于对向量\(x\)施加了\(n-k\)个约束. 因此为了保证有解,在下面构造\(x\)的时候取了\(n-k+1\)个自由度.

根据上述论述, 存在\(c_1,c_2,\cdots, c_{n-k+1}\)使得\(x=c_1 x_1+\cdots  c_{n-k+1}x_{n-k+1}\), 此时:

\[R(x)=\frac{\lambda_1c_1^2+\cdots+\lambda_{n-k+1}c_{n-k+1}^2}{c_1^2+\cdots+c_{n-k+1}^2}\le\lambda_{n-k+1}\]

容易验证当\(V_{k}=span\\{x_{n-k+1},\cdots, x_{n}\\}\)时, 上式取到最大值\(\lambda_{n-k+1}\).





