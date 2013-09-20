---
layout: post
title: 复数基础
date: '2013-09-14'
description: 复数的定义、几何解释、加减法、乘除法。
categories: "Analysis"
tags: [Complex number, Trigonometric]
mathjax: true
---

复数理论的建立，就是数学上的一次推广。就像是数学刚刚发展时正整数不够用，推广出了负整数；整数不够用，推广产生了有理数；接下来人们发现，其实还有不可公度的线段，于是无理数产生。然而，这样的推广一定要与推广前的数学相合。

复数的发明，决不是某个人的成果，而是整个数学界的需要。最早的需要是解二次方程，像 $x^2 + 1 = 0$ 这样的方程，如果仅仅限于在实数范围内解，我们很容易就会说它“没有实数根”。

可是，我们可以用我们的方法扩充数，使方程有解。于是我们就定义虚数单位 $i = \sqrt{1}$ 或 $i^2 = -1$，然而这完全是一个符号，这个定义的有用程度取决于我们用这个定义发展出的数学理论是否有用。

我们自然希望这个东西要服从原有的数的运算法则。于是，我们就希望可以用 $3i$ 或 $\sqrt{2}i$ 这样对 $i$ 进行加减乘除，甚至造出像 $2 + i$ 这样的数，或用 $a + b i$ 这样的符号（这里 $a$ 被叫做实部，$b$ 被叫做虚部）。它还要服从加法和乘法的交换律、分配律和结合律：

$$
\begin{eqnarray*}
  (2 + 3i) + (1 + 4i) &=& (2 + 1) + (3 + 4)i \\
                      &=& 3 + 7i \\
  (2 + 3i)(1 + 4i)    &=& 2 + 8i + 3i + 12i^2 \\
                      &=& (2-12) + (8 + 3)i \\
                      &=& -10 + 11i
\end{eqnarray*}
$$

同时，复数的相除也有意义：

$$
\begin{eqnarray*}
  \frac{2 + 3i}{1 + 4i} &=& \frac{(2 + 3i)(1 - 4i)}{(1 + 4i)(1 - 4i)} \\
                        &=& \frac{14 - 5i}{17}
\end{eqnarray*}
$$

这样，复数之间的加减乘除得出的仍是复数，这当然是我们想要的结果。

<!--more-->

接下来谈到的是复数的几何解释。实数可以与数轴一一对应，这是实数的几何解释方法。而在复数没有几何解释之前，人们认为这个“虚数”是个虚构或不实际的东西。

这个几何解释，就是把复数与平面联系起来。我们取一个直角坐标系，并用点 $(x, y)$ 表示复数 $z = x + yi$。$z$ 的实部 $x$ 表示它的 $x$ 坐标，虚部 $y$ 表示它的 $y$ 坐标。因此在复数与平面上的点中产生了一个一一对应的关系。

{% tikz 复数与平面的对应 :name complex %}
\draw[->] (-1, 0) --(5, 0) node (xaxis) [below] {$x$};
\draw[->] (0, -1) --(0, 5) node (yaxis) [right] {$y$};
\coordinate [label=below left:{$O$}] (O) at (0,0);
\draw (O) --(3, 4) node (z) [above] {$z = x + yi$};
{% endtikz %}

我们还可以定义共轭复数：

$$ \overline{z} = x - yi $$

在复平面上用点 $z$ 关于 $x$ 轴的镜面反射来表示 $\overline{z}$。

我们用 $\rho = \sqrt{x^2 + y^2}$ 来表示 $z$ 到原点的距离，又称为复数 $z$ 的**模**，记作 $\rho = |z|$。我们还能得到这样一个结果：

$$
\rho^2 = x^2 + y^2 = (x + yi)(x - yi) = z \cdot \overline{z}
$$

同时我们定义幅角 $\varphi$ 为 $zO$ 与 $x$ 轴正方向的夹角。

{% tikz 复数的幅角，模与共轭 :name complex2 %}
\draw[->] (-1, 0) --(5, 0) node (xaxis) [below] {$x$};
\draw[->] (0, -5) --(0, 5) node (yaxis) [right] {$y$};
\coordinate [label=below left:{$O$}] (O) at (0, 0);
\coordinate [label=right:{$\rho$}] (rho1) at (1.5, 2);
\coordinate [label=right:{$\rho$}] (rho2) at (1.5, -2);
\coordinate [label=above right:{$\varphi$}] (phi) at (0.5, 0);
\coordinate [label=below right:{$-\varphi$}] (phi) at (0.5, 0);
\draw (O) --(3, 4) node (z1) [above] {$z = x + yi$};
\draw (O) --(3, -4) node (z2) [below] {$\overline{z} = x - yi$};

{% endtikz %}

两个复数 $z_1 = x_1 + y_1 i$ 与 $z_2 = x_2 + y_2 i$ 的相加的定义，我们能得到：

$$
z_1 + z_2 = (x_1 + x_2) + (y_1 + y_2)i
$$

因此在复平面上复数的和 $z_1 + z_2$ 是遵守平行四边形法则的。

最后要谈的是两个复数的相乘。把 $z_1$ 和 $z_2$ 表示为 $z_1 = \rho_1(\cos\varphi_1 + i \sin\varphi_1)$ 和 $z_2 = \rho_2(\cos\varphi_2 + i \sin\varphi_2)$。

$$ z_1 \cdot z_2 = \rho_1\rho_2[(\cos\varphi_1\cos\varphi_2 - \sin\varphi_1\sin\varphi_2) + i(\cos\varphi_1\sin\varphi_2 + \sin\varphi_1\cos\varphi_2)] $$

利用三角函数的和角公式：

$$
\cos\varphi_1\cos\varphi_2 - \sin\varphi_1\sin\varphi_2 = \cos(\varphi_1 + \varphi_2),\\
\cos\varphi_1\sin\varphi_2 + \sin\varphi_1\cos\varphi_2 = \sin(\varphi_1 + \varphi_2)
$$

就能得到：

$$
z_1z_2 = \rho_1\rho_2[\cos(\varphi_1 + \varphi_2) + i \sin(\varphi_1 + \varphi_2)]
$$

于是，我们就能得到，两个复数相乘，就是把它们的模相乘而幅角相加。对于复数的除法，就是把它们的模相除而幅角相减。

{% referencelist %}
{% bibliography --file complex-number-theory.bib %}
