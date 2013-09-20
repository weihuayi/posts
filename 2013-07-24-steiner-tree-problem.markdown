---
layout: post
title: Steiner 问题：光学解法
date: '2013-7-24'
description: 提出 Steiner 问题，并根据光学解 Steiner 问题。
categories: "Geometry"
tags: [Steiner tree problem]
mathjax: true
---

Steiner 问题（Steiner Tree Problem，施泰纳问题）：平面上，给定三角形三个点，求到这三个点距离之和最小的点。

Steiner 问题历史上最初由 Fermart（费马）在十七世纪初提出，在 1640 年之前，这个问题最先被 Torricellis（托里拆利）解决，后来这个问题又发现了多种解决方法。本文主要探讨 Steiner 问题用光学解决的方法。

先做一些准备工作。1662 年，Fermart 提出了 Fermart 原理，说的是光线在传播时会选择时间极短的路径。利用这个原理，我们可以看到，光线在点 $A$ 出发通过镜子通过点 $B$，总是会通过点 $X$。因为光线的速度一致时，它只有在通过点 $X$ 时才会路程极短。利用反证法，如果它通过了另一点 $X'$，根据三角形两边之和大于第三边，会有 $AX' + BX = AX' + B'X' > AX + B'X = AX + BX$，反正路程会更长，违反了 Fermart 原理。这时我们可以看出，$AX$ 和 $BX$ 与反射面的夹角相等。

{% image 1.png %}
steiner problem picture 1
{% endimage %}

<!--more-->

这个问题还有另一个解释方法。这个直线上有一个点 $X$ 使 $AX + BX$ 取极小值 $2a$，我们考虑所有使 $AK + BK = 2a$ 的点的轨迹，根据椭圆的定义：椭圆是平面上所有到两个固定点距离之和相等的点的轨迹。这个点 $K$ 的轨迹显然是个椭圆。

真正有趣的地方在于：这个椭圆必定和直线相切。如果它与直线有两个交点 $P$ 和 $Q$，那么极小值必定在线段 $PQ$ 之间，所以它们不能有两个交点。

我们附带证明了一个重要的几何定理：椭圆上的任意一点与焦点的连线，与在此处的切线夹角相等。

{% image 2.png %}
steiner problem picture 2
{% endimage %}

假设有三个城镇，要建设三条公路到一个交通中心，使公路的总造价最小。它可以抽象为我们在文章开头提出的：平面上，给定三角形三个点，求到这三个点距离之和最小的点。

我们假设 $\triangle ABC$ 是个锐角三角形，因为其它的三角形会有不同的解法。假定 $PC$ 的长不变，以 $C$ 为圆心，$PC$ 长为半径作圆。我们已经知道光线有这样的性质：它会找极短的路径。让点 $P$ 在圆上运动，光线在点 $P$ 处也要遵守反射定律，得到在 $PC$ 延长线平分 $\angle APB$ 时 $AP + BP$ 才取极小值。同时对点 $A$ 和点 $B$ 也这么论证。

{% image 3.png %}
steiner problem picture 3
{% endimage %}

论证的结果是，在下图中，相同颜色的角相等，再注意到对顶角相等，它们每个角都是 $60 ^\circ$，所以得出结论：$AP$，$BP$ 和 $CP$ 之间应该有相等的 $120^\circ$ 夹角。

{% image 4.png %}
steiner problem picture 4
{% endimage %}

参考文献
{% bibliography --file steiner-tree-problem.bib %}
