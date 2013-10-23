---
layout: post
title: "CGAL学习-二维三角形网格优化(4)"
categories: "CGAL"
tags: [triangulation, optimization, c++]
mathjax: true
description: |
   借助前面介绍的　Triangulation_2 模板类，来实现一些标准的三角形网格优化方法：点光滑化和拓扑优化方法（换边）。
---
{% include JB/setup %}

## 三角形网格优化方法简介
三角形优化方法通常分为两类：光滑化方法和拓扑优化方法。前一种方法优化网格节点的坐标位置；后一种方法优化网格节点的连接关系。

### 光滑化方法
给定一个网格节点$X_i$, 设$\{X_j\}_{j=1}^{N}$为与节点$X_i$相邻的节点集合, 
$\{\tau_j\}_{j=1}^{N}$ 为以$X_i$为顶点的三角形集合。下面给出不同光滑方法，新坐标$X_i^{New}$的计算公式。
####　Laplace 光滑

$$
\begin{equation}\lable{eq:L}
X_i^{New} = \frac{1}{Ｎ}\sum\limits_{j=1}^N　X_j.
\end{equation}
$$

####　Centroidal Patch Triangulation(CPT) 光滑

$$
\begin{equation}\lable{eq:L}
X_i^{New} = \frac{1}{Ｎ}\sum\limits_{j=1}^N　b_j.
\end{equation}
$$

其中$b_j$为$\tau_j$的质心。

####   Optimal Delaunay Triangulation(ODT) 光滑

$$
\begin{equation}\lable{eq:L}
X_i^{New} = \frac{1}{Ｎ}\sum\limits_{j=1}^N　c_j.
\end{equation}
$$

其中$c_j$为$\tau_j$的外接圆圆心。

####   Lloyd 光滑

###　拓扑优化方法

##　练习
基于　Triangulation_2 模板类实现上述优化方法,　并对网格例子进行优化,　比较优化结果。

