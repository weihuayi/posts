---
layout: post
title: "稀疏矩阵存储格式"
categories: "math"
tags: [sparse matrix]
mathjax: true
description: |
   本文介绍稀疏矩阵常用的两种存储格式: 压缩行存储(Compressed Row
   Storage, [CRS][CRS])和压缩列存储(Compressed Column Storage, [CCS][SM]).

---
{% include JB/setup %}

给定 $n$ 阶矩阵 $A$ , 如果其非零元的个数比较少, 我们就称其[**稀疏矩阵
**][SM]. 这样在计算机中存储 $A$ 时, 如果每个元素都存下来, 是很浪费存储空间
的. 比如一个 10 万阶的矩阵, 就有 $10^{10}$ 个元素, 假设其中只有 10 万个
非零元. 每个元素如果用双精度存储的话, 要占 8 个字节, 把所有的元素存储
下来, 大概要占多大空间呢?

$$
\begin{eqnarray} 
\frac{\mbox{10 万阶矩阵的字节数}}{\mbox{1
GB 的字节数}} = \frac{10^5\times 10^5\times
8}{2^{10}\times 2^{10}\times 2^{10}} = 74.5 (GB),
\end{eqnarray}
$$

对一般中小规模的计算机, 这是很难以承受的. 但如果用本节介绍的 CRS 或者
CCS, 就可以大大节省存储空间.


下面以一个具体的矩阵为列进行说明:

$$
A = 
\begin{pmatrix}
0 & 0 & 0 & 10 \\
21 & 0 & 33 & 0 \\
0  & 0 & 3  & 0 \\
12 & 1 & 0 & 4 
\end{pmatrix}
$$

这里我们采用 C\C++ 的习惯, 编号都从 0 开始. 则**压缩行存储**可以用下面三个数组来表示这个矩阵

$$
\begin{eqnarray}
row_{ptr} &=& [0,1,3,4,7] \\
col_{idx} &=& [3,0,2,2,0,1,3] \\
val &=& [10,21,33,3,12,1,4]
\end{eqnarray}
$$

压缩列存储可以用下面三个数组来表示这个矩阵:

$$
\begin{eqnarray}
col_{ptr} &=& [0,2,3,5,7] \\
row_{idx} &=& [1,3,3,1,2,0,3] \\
val &=& [21,12,1,33,3,10,4]
\end{eqnarray}
$$


还以上面的 10 万阶的矩阵为例, 它有 10 万个非零元, 在 CRS 模式下, 它占
的内存为(以 MB 为单位):

$$
\begin{eqnarray} 
\frac{(10^5\times 3 + 1)\times 8}{2^{10}\times 2^{10}\times 2^{10}} \approx
2.29 (MB),
\end{eqnarray}
$$

哈哈, 内存节省了 10 万倍.


[CRS]: http://de.wikipedia.org/wiki/Compressed_Row_Storage "Compressed Row Storage"

[SM]: http://en.wikipedia.org/wiki/Sparse_matrix "Sparse Matrix"


