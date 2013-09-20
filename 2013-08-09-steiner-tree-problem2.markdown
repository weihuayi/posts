---
layout: post
title: Steiner 问题：力学解法
date: '2013-08-09'
description: 根据力学的平衡时系统势能最小和物体的受力平衡解 Steiner 问题。
categories: "Geometry"
tags: [Steiner tree problem]
mathjax: true
---

在说过 Steiner 问题的[光学解法](/mathematics/steiner-tree-problem.html)之后，我们再来谈谈它的力学解法。首先关注这么一个问题：

{% problem %}
已知一条绳子，两端分别固定在点 $A$ 和点 $B$ 上，绳子上有一可以移动的铁环，求它的平衡位置。
{% endproblem %}

我们假设绳子是光滑的，不可伸长，没有重量，铁环的尺寸可以忽略，当成是一个点 $X$。

同时注意到两点：

 - 根据物理定律，环必定要处在它能做到的最低点。因为绳不能伸长，所以在以点 $A$ 和点 $B$ 为焦点的椭圆上，点 $X$ 处的切线必定是水平的，否则它不是最低点。

 - 在点 $X$ 处的受力必须平衡。环的重力 $G$、绳子的张力都作用在 $X$ 点，力学指出，$AX$ 和 $BX$ 处的张力的大小相等。再根据点 $X$ 处的受力平衡，两个张力的合力必须与环的重力是平衡力。于是合力平分 $\angle AXB$，且垂直于椭圆的水平切线。

<!--more-->

{% tikz :name picture1 %}
\newcommand\ellipsebyfoci[4]{
  \path[#1] let \p1=(#2), \p2=(#3), \p3=($(\p1)!.5!(\p2)$)
  in \pgfextra{
    \pgfmathsetmacro{\angle}{atan2(\x2-\x1,\y2-\y1)}
    \pgfmathsetmacro{\focal}{veclen(\x2-\x1,\y2-\y1)/2/1cm}
    \pgfmathsetmacro{\lentotcm}{\focal*2*#4}
    \pgfmathsetmacro{\axeone}{(\lentotcm - 2 * \focal)/2+\focal}
    \pgfmathsetmacro{\axetwo}{sqrt((\lentotcm/2)*(\lentotcm/2)-\focal*\focal}
  }
  (\p3) ellipse[x radius=\axeone cm,y radius=\axetwo cm, rotate=\angle];
}
\coordinate [label=below right:{$X$}] (x) at (0, 0);
\coordinate [label=above right:{$A$}] (a) at x + (150:3);
\coordinate [label=above  left:{$B$}] (b) at x + (30:5);
\coordinate (g1) at x + (150:1);
\coordinate (g2) at x + (30:1);
\coordinate [label=left:\textcolor{red}{$G$}](g3) at x + (-90:1);
\coordinate (g4) at x + (90:1);

\draw (a) --(x) --(b);
\draw[red, ->] (x) --(g1);
\draw[red, ->] (x) --(g2);
\draw[red, ->] (x) --(g3);
\draw[red, ->, dashed] (x) --(g4);
\draw[dashed] (g1) --(g4);
\draw[dashed] (g2) --(g4);
\draw (-3, 0) --(4.5, 0);

\ellipsebyfoci{draw}{a}{b}{1.142857};
\fill (a) circle(2pt);
\fill (x) circle(2pt);
\fill (b) circle(2pt);

{% endtikz %}

我们根据这两个方法做出的解必须一致，因此，$XA$ 和 $XB$ 这两条线相对合力的夹角相等，所以它们相对点 $X$ 处的切线也有相等的夹角。我们又重新发现了在光学中提到过的性质。

{% property %}
椭圆上的任意一点与焦点的连线，与在此处的切线夹角相等。
{% endproperty %}

有了这个方法的启发，我们就可以开始着手证明 Steiner 问题了。设想有这样的机械装置，它能够解我们讨论过的 Steiner 问题。

{% problem %}
在墙上三点 $A$，$B$ 和 $C$，它们已经被固定。假设它们固定着三个定滑轮，三条长度固定的绳子分别过这三个点，在公共中心 $X$ 处连结。$A$，$B$ 和 $C$ 下都挂着相等重量的物体。我们的问题是：求它的平衡位置。
{% endproblem %}

{% tikz :name picture2 %}
\coordinate [label=below left:{$X$}] (x) at (0, 0);
\coordinate [label=above:{$A$}] (a) at x + (165:5);
\coordinate [label=above:{$B$}] (b) at x + (45:3);
\coordinate [label=below right:{$C$}] (c) at x + (-75:4);

\draw[->] (x) --(a) to +(0, -1);
\draw[->] (x) --(b) to +(0, -1);
\draw[->] (x) --(c) to +(0, -1);

\fill (a) circle(2pt);
\fill (b) circle(2pt);
\fill (c) circle(2pt);
\fill (x) circle(2pt);

\draw[red, ->] (x) to +(165:1);
\draw[red, ->] (x) to +(-75:1);
\draw[red, ->] (x) to +(45:1);
{% endtikz %}

{% solution %}
我们同样关注这么两点：

 - 记住这个物体要尽可能地接近地面，也就是说，平衡时，系统的势能必将最小，且三个点处的物体重量相等。可以看出，平衡时，$AX + BX + CX$ 取最小值。从而我们的问题与 Steiner 问题等价。

 - 同时，平衡时，点 $X$ 处的受力要平衡。由于三个方向的力大小相等，所以它们要互成 $120 ^\circ$ 角。
{% endsolution %}

参考文献
{% bibliography --file steiner-tree-problem.bib %}
