---
layout: post
title: How does FFT work?
---
{% raw %}
Let's first start with DFT (Discrete Fourier Transform)

$$
\begin{bmatrix}
y_1\\\
y_2\\\
y_3\\\
\vdots\\\
y_n
\end{bmatrix}=
\begin{bmatrix}
1 & 1 & 1 & \cdots & 1 \\\
1 &  \omega & \omega^2 &\cdots & \omega^{n-1} \\\
1 & \omega^2 & \omega^4 & \cdots & \omega^{2n-2} \\\
\vdots & \vdots & \vdots & \ddots & \vdots \\\
1 & \omega^{n-1} &\omega^{2n-2} & \cdots & \omega^{(n-1)^2}
\end{bmatrix}
\begin{bmatrix}
c_1\\\
c_2\\\
c_3\\\
\vdots\\\
c_n
\end{bmatrix},\quad \omega=e^{\frac{2\pi i}{n}}
$$

<!--more-->

The vector \\(y\\) is the function to be expanded; it is seen in *frequency space* through the coefficients \\(c_k\\). This formula is actually called the inverse Fourier transform. It can be seen from \\(\\omega\\)(it has positive sign on \\(\omega\\)). Fourier transform is the one that computes the frequency expansion given the function value at each time step.

Compare to the continuous form of Fourier transform:

$$
f(t)=\int_{-\infty}^{+\infty}F(\nu)e^{2\pi i\nu t}d\nu
$$

In the n order Fourier matrix, we have to compute 

$$
y_j=\sum_{k=0}^{n-1}\omega^{jk}x_k, \quad j=0,1,\cdots,n-1
$$

The complexity is \\(O(n^2)\\). The idea of FFT is to recursively compute the half size matrix (i.e. \\(F_{n/2}, F_{n/4}, \cdots\\)) and the complexity can be reduced to \\(O(nlog(n))\\).
The link between the origin matrix and its half sized counterpart is the property of complex number. Suppose \\(m=\frac{n}{2}\\), then \\(\omega_m=\omega_n^2\\) (It's easy to see, since the m-order unit roots separate the unit circle into m parts.) 
For the first m entries of \\(y\\), we split the sum into even and odd parts.
\\[y_j=\sum_{k=0}^{n-1}\omega_n^{jk}c_k=\sum_{k=0}^{n/2-1}\omega_n^{2jk}c_{2k}+\sum_{k=0}^{n/2-1}\omega_n^{j(2k+1)}c_{2k+1}, \quad j=0,1,\cdots, n/2-1\\]
The even c's go into \\(c'=(c_0,c_2,\cdots)\\) and the odd c's go into \\(c''=(c_1,c_3,\cdots)\\). Set \\(y'=F_mc',y'\'=F_mc''\\). Then using \\(\omega_m=\omega_n^2\\), we can transform it into the combintion of \\(y' and y''\\).

$$
LHS=\sum_{k=0}^{m-1}\omega_m^{jk}c'_k + \omega_n^j \sum_{k=0}^{m-1}\omega_m^{jk}c''_k=y'_j+(\omega_n)^jy''_j
$$

For \\(j\ge m\\), Noticing that \\(\omega_n^m=-1\\) we have:

$$
\begin{equation} 
\begin{split}
y_{j+m} & = \sum_{k=0}^{n-1}\omega_n^{(j+m)k}c_{k} \\
& = \sum_{k=0}^{n/2-1}(-1)^{2k}\omega_n^{2jk}c_{2k}+\sum_{k=0}^{n/2-1}(-1)^{(2k+1)}\omega_n^{j(2k+1)}c_{2k+1} \\
& =\sum_{k=0}^{m-1}\omega_m^{jk}c'_k - \omega_n^j \sum_{k=0}^{m-1}\omega_m^{jk}c''_k \\
& = y'_j - (\omega_n)^j y''_j 
\end{split}
\end{equation}
$$

So here we are, the essential expansion in this recursion.

$$
\begin{align}
y_j=y'_j+\omega_n^jy''_j, \quad j=0,1,\cdots,m-1 \\
y_{j+m}=y'_j-\omega_n^jy''_j, \quad j=0,1,\cdots,m-1
\end{align}
$$

The equations can be written in matrix expression.

$$
y=
\begin{bmatrix}
I_m & D_m \\
I_m & -D_m
\end{bmatrix}
\begin{bmatrix}
y'\\
y''
\end{bmatrix}, \quad D_m=diag(1,\omega,\cdots, \omega^{m-1})
$$

Remember the definition of \\(y' and y''\\).

$$
\begin{bmatrix}
y'\\y''
\end{bmatrix}=
\begin{bmatrix}
F_m &O\\
O&F_m
\end{bmatrix}
\begin{bmatrix}
c'\\c''
\end{bmatrix}
$$

We are nearly there; the last matrix is an 'even-odd' permutation that separates the incoming vector \\(c\\) into its even and odd parts \\(c'=(c_0,c_2,\cdots,c_{n-2}) and c''=(c_1, c_3,\cdots,c_{n-1})\\). For a direct look, we give the example of a 4-order even-odd permutation matrix:

$$
P_4=\begin{bmatrix}
1 &&&\\
&&1&\\
&1&&\\
&&&1
\end{bmatrix}
$$

So one recursion of the FFT can be written as the multiplication of three matrix.

$$
F_n=
\begin{bmatrix}
I_n/2 & D_n/2 \\
I_n/2 & -D_n/2
\end{bmatrix}
\begin{bmatrix}
F_n/2&O\\
O& F_n/2
\end{bmatrix}
P_n
$$

The whole algorithm will iteratively compute \\(log_2(n)\\) stages until it reaches the bottom. In each stage, The only computation is the multiplication between the diagonal matrix and the half sized Fourier matrix, which is \(\frac{n}{2}\\) times of multiplications. So the whole algorithm will take \\(\frac{1}{2}nlog_2n\\) computation.

As for the multiplication of the permutation, there is an elegant way of addressing it. Write the number 0 to n-1 in binary,  and resort them while reversing the order of their bits. Below shows an example of n=8.

$$
\begin{matrix}
input& binary& reversed & output\\
0& 000& 000 & 0\\ 
1& 001& 100& 4\\
2& 010& 010& 2\\
3& 011& 110& 6\\
4& 100& 001& 1\\
5& 101& 101& 5\\
6& 110& 011& 3\\
7& 111& 111& 7\\
\end{matrix}
$$
{% endraw %}