---
layout: post
title: Heron 公式，Brahmagupta 公式及应用
date: '2013-08-18'
description: 证明了 Heron 公式和 Brahmagupta 公式，把它应用在证明等边三角形和正方形的同周长时面积最大性质。
categories: "Geometry"
tags: [Heron's formula, Brahmagupta's formula, Bretschneider's formula]
mathjax: true
---

[Heron 公式](http://en.wikipedia.org/wiki/Heron\'s_formula)（海伦－秦九韶公式） $A = \sqrt{p(p - a)(p - b)(p - c)}$ 指出了三角形的面积 $A$ 与它的半周长 $p = (a + b + c)/2$ 之间的联系。

{% tikz :name heron %}
\coordinate [label=left:{$A$}] (a) at (-3, 0);
\coordinate [label=right:{$B$}] (b) at (3, 0);
\coordinate [label=above right:{$C$}] (c) at (1.5, 3);
\coordinate [label=above right:{$a$}] (la) at ($ (b)!0.5!(c) $);
\coordinate [label=above left:{$b$}] (lb) at ($ (a)!0.5!(c) $);
\coordinate [label=below:{$c$}] (lc) at ($ (a)!0.5!(b) $);

\fill (a) circle(2pt);
\fill (b) circle(2pt);
\fill (c) circle(2pt);

\draw (a) --(b) --(c) --cycle;
{% endtikz %}

<!--more-->

{% prove %}
设边 $a$ 与边 $b$ 的夹角是 $\phi = \angle C$，余弦定理和三角形面积公式指出：

$$
  \begin{eqnarray*}
    a^2 + b^2 - c^2 & = & 2ab \cos{\phi}\\
    2A & = & ab \sin{\phi}
  \end{eqnarray*}
$$

两式同时平方，得：

$$
  \begin{eqnarray*}
    (a^2 + b^2 - c^2)^2 & = & 4a^2b^2 \cos{\phi} \\
    16 A^2 & = & 4a^2 b^2 \sin^2{\phi}
  \end{eqnarray*}
$$

两式相加，运用平方差公式：

$$
\begin{eqnarray*}
16 A^2 & = & 4a^2b^2 - (a^2 + b^2 - c^2)^2 \\
       & = & (2ab + a^2 + b^2 - c^2)(2ab - a^2 - b^2 + c^2) \\
       & = & [(a + b)^2 - c^2][c^2 - (a - b)^2] \\
       & = & (a + b + c)(a + b -c)(c + a - b)(c + b -a) \\
       & = & 2p (2p - 2c)(2p - 2b)(2p - 2a) \\
       & = & 16 p (p - a)(p - b)(p - c)
\end{eqnarray*}
$$

简单的变换后，公式就证明出来了。
{% endprove %}

Heron 公式可以用在证明等边三角形的这一性质：

{% property %}
在所有周长相等的三角形中，以等边三角形的面积最大。
{% endproperty %}

{% prove %}
把 Heron 公式平方，用平均值不等式：

$$ 
\begin{eqnarray*}
A^2 & =   & p (p - a) (p - b) (p - c) \\
    & \leq & \Big( \frac{p + p - a + p - b + p - c}{4} \Big)^4 \\
    & =   & (p / 2)^4
\end{eqnarray*}
$$

要使不等式取等号，就要有 $a = b = c$。

这个命题还有个等价形式：在所有面积相等的三角形中，以等边三角形的周长最小。
{% endprove %}

其实 Heron 公式可以推广到圆内接四边形的情形中，这个公式叫 [Brahmagupta 公式](http://en.wikipedia.org/wiki/Brahmagupta\'s_formula) （婆罗摩笈多公式）。

{% theorem %}
在圆内接四边形 $ABCD$ 中，有公式 $A=\sqrt{(s-a)(s-b)(s-c)(s-d)}$ 成立。
{% endtheorem %}

{% tikz :name brahmagupta %}
\coordinate [label=right:{$A$}] (a) at (0:3);
\coordinate [label=above right:{$B$}] (b) at (70:3);
\coordinate [label=below left:{$C$}] (c) at (-140:3);
\coordinate [label=below right:{$D$}] (d) at (-60:3);

\coordinate [label=left:{$a$}] (la) at ($ (b)!0.5!(c) $);
\coordinate [label=below:{$b$}] (lb) at ($ (c)!0.5!(d) $);
\coordinate [label=left:{$c$}] (lc) at ($ (a)!0.5!(d) $);
\coordinate [label=below left:{$d$}] (ld) at ($ (a)!0.5!(b) $);

\draw (0, 0) circle(3);

\fill (a) circle(2pt);
\fill (b) circle(2pt);
\fill (c) circle(2pt);
\fill (d) circle(2pt);

\draw (a) --(b) --(c) --(d) --cycle;
{% endtikz %}

{% prove %}
这个定理的基本思想和前一个是一样的。设 $a$ 与 $b$ 的夹角是 $\phi = \angle C$，$c$ 与 $d$ 的夹角是 $\psi = \angle A$。可得： 

$$
\begin{equation}
2A = ab \sin{\phi} + cd \sin{\psi}
\label{eq:2a}
\end{equation}
$$

用两种方法表示四边形中 $\phi$ 和 $\psi$ 共同所对的对角线 $\delta$。

$$
  \begin{eqnarray*}
    \delta^2 & = & a^2 + b^2 - 2 ab \cos{\phi} \\
    \delta^2 & = & c^2 + d^2 - 2 cd \cos{\psi}
  \end{eqnarray*}
$$

变换后得出：

$$
\begin{equation}
a^2 + b^2 - c^2 - d^2 = 2 ab \cos{\phi} - 2 cd \cos{\psi}
\label{eq:2b}
\end{equation}
$$

由 ($\ref{eq:2a}$) 和 ($\ref{eq:2b}$) 的共同平方得出：

$$
\begin{eqnarray}
(a^2 + b^2 - c^2 - d^2)^2 & = & 4 a^2 b^2 \cos^2{\phi} + 4 c^2 d^2 \cos^2{\psi \label{eq:2c}} \\
                          &   & - 8 abcd \cos{\phi} \cos{\psi} \nonumber \\
                   16 A^2 & = & 4 a^2 b^2 \sin^2{\phi} + 4 c^2 d^2 \sin^2{\psi} \label{eq:2d} \\
                          &   & + 8 abcd \sin{\phi} \sin{\psi} \nonumber
\end{eqnarray}
$$

两式相加，运用三角学的公式：$- \cos{\phi}\cos{\psi} + \sin{\phi}\sin{\psi} = - \cos({\phi + \psi})$，同时已知共圆，$\cos({\phi + \psi}) = \cos{\pi} = 1$。

$$
\begin{equation}
  16 A^2 + (a^2 + b^2 - c^2 - d^2)^2 = 4(ab + cd)^2
\end{equation}
$$

其余的和上一个证明一样，不再说了。
{% endprove %}

其实这个公式还可以再推广为任意四边形的情形，叫 [Bretschneider 公式](http://en.wikipedia.org/wiki/Bretschneider\'s_formula)（布雷特施奈德公式，感谢 graphbuster），这个证明出自 {% cite mapr-cn %} 例 8.41。

{% theorem %}
在任意一个四边形中，设两个对角的和 $\varepsilon = \phi + \psi$ 已知，则有 $A^2 = (p - a)(p - b)(p - c)(p - d) - abcd \cos^2{\varepsilon / 2}$
{% endtheorem %}

{% prove %}
($\ref{eq:2c}$)($\ref{eq:2d}$) 相加，注意三角学的和角公式和半角公式。

$$
\begin{eqnarray*}
16 A^2 + (a^2 + b^2 - c^2 - d^2)^2 & = & 4 a^2 b^2 + 4 c^2 d^2 - 8 abcd \cos{\varepsilon} \\
                                   & = & 4 (ab + cd)^2 - 16 abcd(\cos{\varepsilon / 2})
\end{eqnarray*}
$$

其余的不用再说了吧，简单的变换后，有 $$A^2 = (p - a)(p - b)(p - c)(p - d) - abcd (\cos{\varepsilon / 2})^2$$
{% endprove %}

同样地，这个公式还可以证明正方形的这个性质：

{% property %}
在所有周长相等的四边形中，以正方形的面积最大。
{% endproperty %}

{% prove %}
同样的方法

$$
\begin{eqnarray*}
  A^2 & \leq & (p - a)(p - b)(p - c)(p - d) \\
      & \leq & \Big( \frac{p - a + p - b + p - c + p -d}{4} \Big)^4 \\
      & =    & (p / 2)^4
\end{eqnarray*}
$$

要使两个不等式取等号，必须有 $\varepsilon = \pi$ 和 $a = b = c = d$，所以这个四边形必须是正方形。
{% endprove %}

{% referencelist %}
{% bibliography --cited %}
