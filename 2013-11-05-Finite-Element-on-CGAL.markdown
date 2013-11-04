---
layout: post
title: "CGAL学习-二维有限元(5)"
categories: "CGAL"
tags: [FEM, Eigen, CGAL]
mathjax: true
description: |
   基于CGAL的三角形数据结构, 实现线性有限元求解 Possion 方程的程序.
---
{% include JB/setup %}

##问题模型

考虑如下D氏边界条件的Poisson方程:

$$
\begin{eqnarray}
-\Delta u(x) &=& f(x),\text{ on } \Omega.\label{eq:P}\\
u|_{\partial\Omega} &=& 0.
\end{eqnarray}
$$


##Galerkin方法
有限元方法是一种基于 PDE (partial differential equations) 的变分形式 (variational formulation) 求解PDE近似解的方法.

给定一个边界恒为零函数$v$, 同乘以方程$\eqref{eq:P}$的两端, 然后做分部积分可得: 

$$
\int_{\Omega}\nabla u\cdot\nabla v\mathrm{d}x = \int_{\Omega}fv\mathrm{d}x.
$$

当然上面的分部积分要想成立, $v$还必须**足够光滑**--函数本身及其一阶导数都在$\Omega$上$L^2$可积, 满足该条件的函数组成
一函数空间, 记$H_0^1(\Omega)$.

原问题就转化为: 求解 $u\in H_0^1(\Omega)$, 满足

$$
\begin{equation}\label{eq:W}
a(u,v) = <f,v> \text{ for all }v\in H_0^1(\Omega).
\end{equation}
$$

其中

$$
a(u,v) = \int_{\Omega}\nabla u\cdot\nabla v\mathrm{d}x, <f,v> =  \int_{\Omega}fv\mathrm{d}x.
$$

下面我们考虑所谓Galerkin方法来求$\eqref{eq:W}$的逼近解. 上面$H_0^1(\Omega)$是一个无限维的空间,
为了把无限维的问题转化为有限维的问题, 引入$H_0^1(\Omega)$的一个有限维的子空间$V_h$, 比如
$V_h=\mathrm{span}\{\phi_1,\phi_2,\ldots,\phi_N\}$. 对任何$v\in V_h$, 它都有唯一的表示

$$
v = \sum\limits_{i=1}^N v_i\phi_i.
$$

可以看出空间$V_h$和$N$维向量空间$\mathbb{R}^N$是同构的, 即

$$
v = \sum\limits_{i=1}^N v_i\phi_i\leftrightarrow\mathbf{v} =(v_1,v_2,\ldots,v_N)^t
$$

其中列向量$\mathbf{v}$是$v$在基$\{\phi_i\}_{i=1}^N$的坐标. 引入**刚度矩阵**(stiff matrix)

$$
\mathbf{A}=(a_{ij})_{N\times N} \text{ with } a_{ij}=a(\phi_i,\phi_j).
$$

和**载荷矢量**(load vector) $\mathbf{f} = (f_1, f_2,\ldots,f_N), f_i=<f,\phi_i>$. 则通过求解如下的
线性代数系统

$$
\mathbf{Au} = \mathbf{f}.
$$

获得解向量$\mathbf{u}=(u_1,u_2,\ldots,u_N)^t$, 对应的有限元解为

$$
u_h = \sum\limits_{i=1}^N u_i\phi_i.
$$

##三角形网格和重心坐标

给定三个不在同一条直线上的二维点$\mathbf{x}_1 :=(x_1,y_1)$, $\mathbf{x}_2 :=(x_2,y_2)$和$\mathbf{x}_3 :=(x_3,y_3)$, 则向量$\mathbf{x}_1\mathbf{x}_2$和$\mathbf{x}_1\mathbf{x}_3$线性无关. 这等价于矩阵

$$
A = 
\begin{pmatrix}
x_1 & x_2 & x_3 \\
y_1 & y_2 & y_3 \\
1   & 1   & 1 
\end{pmatrix}
$$

非奇异. 任给一点$\mathbf{x}:=(x,y)$, 求解下面的线性方程组

$$
A 
\begin{pmatrix}
\lambda_1 \\
\lambda_2\\
\lambda_3  
\end{pmatrix}
=\begin{pmatrix}
x \\
y\\
1  
\end{pmatrix}
$$

可得唯一的一组解$\lambda_1,\lambda_2,\lambda_3$, 因此对任意二维点$\mathbf{x}$, 有

$$
\mathbf{x}=\lambda_1(\mathbf{x})\mathbf{x}_1 + \lambda_2(\mathbf{x})\mathbf{x}_2 + \lambda_3(\mathbf{x})\mathbf{x}_3 
\text{ with } \lambda_1(\mathbf{x}) + \lambda_2(\mathbf{x}) + \lambda_3(\mathbf{x}) = 1. 
$$

$\lambda_1,\lambda_2,\lambda_3$称为点$\mathbf{x}$关于点$\mathbf{x}_1,\mathbf{x}_2$和$\mathbf{x}_3$的**重心坐标**. 重心坐标
有它相应的几何意义. 记$\mathbf{x}_1,\mathbf{x}_2$和$\mathbf{x}_3$组成的三角形为$\tau$, 把$\tau$的顶点$\mathbf{x}_i$换$\mathbf{x}$
得到的三角形记为$\tau_i(\mathbf{x})$, $i=1,2,3$, 则由克莱姆法则可得

$$
\lambda_i = {|\tau_i(\mathbf{x})| \over |\tau|}.
$$

其中$|\cdot|$表示三角形的面积.




##稀疏矩阵和向量

在CGAL中, 已经定义两个wrapper类, 把Eigen中的稀疏矩阵和向量的接口封装起来, 见头文件:

```cpp
#include <CGAL/Eigen_matrix.h>
#include <CGAL/Eigen_vector.h>
```

下面的代码为CGAL中的这两个wrapper类, 创建一个新的简短的名字:

```cpp
typedef CGAL::Eigen_sparse_symmetric_matrix<double> ESMatrix;
typedef CGAL::Eigen_vector<double> EVector;
```

其中`ESMatrix`表示一个稀疏的对称矩阵, 只存储矩阵的下三角部分. 下面定义一个$n\times n$的`ESMatrix`矩阵 $m$:

```cpp
ESMatrix  m(n);//默认所有位置的元素值为0
```

下面的代码等价于 $m(i,j) = m(i,j) + val$;

```cpp
int i = ...;
int j = ...;
double val = ...;
m.add_coef(i,j,val);
```

其中`EVector`表示稠密向量. 下面定义一个$n$维的'EVector'零向量$v$, 并对其分量进行相应的运算:

```cpp
EVector v(n);
int i = ...;
double val = ...;
v(i) = val; //v(i)的值设为 val
v(i) += val; //v(i)的值累加val 
```

当使用有限元方法离散上面的Poisson方程, 并进行边界处理后, 得到离散系统$AX=b$, 然后就可以调用Eigen中的
解法器进行求解, 比如:

```cpp
typedef Eigen::BiCGSTAB<ESMatrix, Eigen::Lower> Solver;
x = solver.compute(A.eigen_object()).solve(b.eigen_object());
if(solver.info()!=Success) {
  std::cout<<"solving failed"<<std::endl;
  return;
}
```



