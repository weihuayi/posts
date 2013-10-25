---
layout: post
title: "CGAL学习-二维三角形网格优化(4)"
categories: "CGAL"
tags: [triangulation, optimization, c++]
mathjax: true
description: |
   借助前面介绍的　Triangulation_2 &lt Traits,TDS &gt 模板类，来实现一些标准的三角形网格优化方法：点光滑化和拓扑优化方法（换边）。
---
{% include JB/setup %}

##三角形网格优化方法简介
三角形优化方法通常分为两类：光滑化方法和拓扑优化方法。前一种方法优化网格节点的坐标位置；后一种方法优化网格节点的连接关系。

###光滑化方法
给定一个网格节点$x_i$, 设$\{ x_j\}_{j=1}^{N_i}$为与节点$x_i$ 相邻的节点集合, 
$\{\tau_j\}_{j=1}^{N}$ 为以$x_i$为顶点的三角形集合。下面给出不同光滑方法，新坐标$x_i^{New}$的计算公式。

####Laplace 光滑

$$
\begin{equation}\label{eq:L}
x_i^{New} = \frac{1}{Ｎ_i}\sum\limits_{j=1}^{N_i}　x_j.
\end{equation}
$$

####Centroidal Patch Triangulation(CPT) 光滑

$$
\begin{equation}\label{eq:CPT}
x_i^{New} = \frac{1}{Ｎ_i}\sum\limits_{j=1}^{N_i}　b_j.
\end{equation}
$$

其中$b_j$为$\tau_j$的质心。

####Optimal Delaunay Triangulation(ODT) 光滑

$$
\begin{equation}\label{eq:ODT}
x_i^{New} = \frac{1}{Ｎ_i}\sum\limits_{j=1}^{N_i}　c_j.
\end{equation}
$$

其中$c_j$为$\tau_j$的外接圆圆心。

####Lloyd 光滑
Lloyd光滑是基于 Centroidal Voronoi tessellation （CVT）导出的光滑方法。给定区域$\Omega\subset R^n$,对于点集
${\bf z}=\{ z_i\}_{i=1}^N\subset\Omega$中的每个点$z_i$， 可定义它的 Voronoi 区域（Voronoi Region）如下

$$
\begin{equation}\label{eq:VR}
V_i:=\{ x\, |\, |x - z_i| < |x - z_j| \text{ for } j\neq i \}
\end{equation}
$$

${\bf V} = \{V_i\}_{i=1}^{N}$称为 Voronoi Tesselation (VT), 点集$\bf z$称为该VT的生成子(generators)。如果VT中
每个Voronoi区域的生成子恰好是它的质心，则称该VT为CVT。基于生成子$\bf z$和$\bf V$可以定义如下的能量泛函

$$
\begin{equation}\label{eq:CVTE}
\mathcal{E}({\bf z},{\bf V}({\bf z})) = \sum\limits_{i=1}^N\int_{V_i}\rho(x)\|{x-z_i}\| {\rm d}x
\end{equation}
$$

其中$\rho(x)$是一个给定的密度函数。一个CVT是能量泛函$\mathcal{E}$的一个**临界点**(Critical Point)，
而一个**稳定**的CVT是$\mathcal{E}$的一个局部极小值。$\mathcal{E}$对$z_i$求导数，可得：

$$
\mathcal{F}_i:=\frac{\partial}{\partial z_i}\mathcal{E}({\bf z},{\bf V}({\bf z})) = 2\int_{V_i}\rho(x)(z_i-x)
{\rm d}x
$$

取$\mathcal{F}_i=0$, 可得：

$$
z_i= \frac{\int_{V_i}\rho(x)x{\rm d}x}{\int_{V_i}\rho(x){\rm d}x}.
$$

引入**Lloyd map**${\bf T}:=(T_1,T_2,\ldots,T_N)$, 其中$T_i$定义如下：

$$
T_i(z_i)= \frac{\int_{V_i}\rho(x)x{\rm d}x}{\int_{V_i}\rho(x){\rm d}x}.
$$

给定一组初始的生成子${\bf z}_0$, Llyod光滑方法定义如下：

1. 构造${\bf V}_k({\bf z}_k)$.
2. 更新${\bf z}_{k+1}={\bf T}({\bf z}_k)$.

###拓扑优化方法

三角形网格的拓扑优化是通过**换边**实现的. 当两信相邻三角形组成一个凸四边形，就可以进行换边，见下图：

{% image cgal/edgeflip.png %}
[Edge flip](http://dit-archives.epfl.ch/SCR96/scr8-page4.html).
{% endimage %}

为了优化拓扑，可以依据不同的准则来换边，如

1. Delaunay准则：两个相邻三角形对角之和小于180.
2. 使得每个内部节点周围的度尽量接近6. 

##练习
基于　Triangulation_2 模板类实现上述优化方法,　并对网格例子进行优化,　比较优化结果。

