---
layout: post
title: 三角形与圆
date: '2013-07-17'
description: 三角形的内切圆、外接圆和旁切圆之间的联系：Euler 公式。
categories: "Geometry"
tags: [Cycle, Euler's formula]
mathjax: true
---

三角形的内切圆，外接圆和旁切圆无疑是初等数学的重要研究对象。其中，内切圆圆心是三角形三条角平分线的交点，即内心；外接圆圆心是三角形三条边的垂直平分线的交点，即外心；旁切圆圆心是三角形一条内角角平分线与两条外角角平分线的交点，叫旁心。

在三种“心”当中，旁心比较特殊，有三个，而内心，外心各只有一个。三种心看似并无关系，实则有内在的联系。

这就是 Euler 公式。

$$
\begin{equation}
2Rr=R^2-d^2
\label{eq:euler}
\end{equation}
$$

其中，$R$ 表示外接圆半径，$r$ 为内切圆半径，$d$ 为两圆的圆心距离。

![Euler theorem figure 1](/img/cyclic-theorem/EulerIO1.gif)

<!--more-->

证明：$\triangle ABC$ 的外切圆圆心和内接圆圆心分别为 $O$ 和 $I$，连接 $AI$ 并延长与 $\odot O$ 交于点 $K$，再连接 $KO$ 并延长交 $\odot O$ 于点 $K'$。延长 $OI$ 成为直径 $UV$。

根据相交弦定理，
$$
\begin{equation}
AI\cdot IK=IU\cdot IV=(R+d)(R-d)=R^2-d^2
\label{eq:chords}
\end{equation}
$$

接下来，在$\triangle ICK$ 中，$\angle CIK$ 是 $\triangle ACI$ 的外角，因此可以看出 $$\angle CIK=\frac{1}{2}(\angle BAC + \angle ACB)$$
同时 $$\angle ICK=\angle BCI + \angle BCK = \frac{\angle ACB}{2} + \angle BAK = \frac{(\angle ACB + \angle BAC)}{2} = \angle CIK$$
于是 $IK=KC$。

另一方面，让点 $Z$ 是三角形和内接圆在 $AB$ 的切点，由于 $\angle ZAI$ 和 $\angle K'$ 都等于 $\frac{1}{2}\angle BAC$，还有一个直角相等，所以有 $\triangle ZAI$ 和 $\triangle CK'K$ 相似，由相似边之比得：
$$\frac{AI}{IZ}=\frac{KK'}{KC}$$

化简得：
$$
\begin{equation}
AI\cdot KC=IZ\cdot KK'=r\cdot 2R
\label{eq:right}
\end{equation}
$$

根据 (\ref{eq:chords}) (\ref{eq:right}) 和 $IK=KC$ 就可以看出 $$2Rr=R^2-d^2$$。

可以导出 Euler 公式的另一形式为 $$\frac{1}{R-d} + \frac{1}{R + d} = \frac{1}{r}$$

这还有个旁心与外心的关系：
$$
\begin{equation}
2Rr_a=d_a^2-R^2
\label{eq:another-euler}
\end{equation}
$$

其中 $r_a$ 是点 $A$ 所对的旁切圆的半径，$d_a$ 是它的圆心与外接圆圆心的距离。

它的证明与上一个证明有相似之处，但是却有了一些细微的变化。

我们没有用到相交弦定理，而用到了切割线定理。

![Euler theorem figure 2](/img/cyclic-theorem/EulerIO2.gif)

点 $K$, $K'$, $V$, $Z$ 与点 $U$ 的作法与上一个相似。作为练习，读者可以自己看一看为什么 $KC = KI_a$。根据切割线定理得，
$$(d_a+R)(d_a-R) = I_aU\cdot I_aV = I_aA\cdot I_aK = I_aA\cdot KC = (I_aZ\cdot \frac{KK'}{KC})\cdot{KC} = r_a \cdot 2R$$

这个公式的另一形式为 $$\frac{1}{d_a - R} - \frac{1}{d_a + R} = \frac{1} {r}$$

内心，外心和旁心还有另一个美丽的关系： $$ II_a^2 = 4R(r_a - r)$$

![Euler addition theorem figure](/img/cyclic-theorem/Euler-addition.png)

证明：如图，只画出点 $O$, $I$, $I_a$, $K$，连接 $OK$ 并延长至点 $O'$ 使 $K$ 是 $OO'$ 的中点。根据余弦定理可得
$$II_a^2 = IO^2 + OI_a^2 - 2\cos{\angle IOI_a}\cdot IO\cdot I_aO$$

$$OO'^2 = IO^2 + IO'^2 - 2\cos{\angle O'IO}\cdot IO \cdot IO'$$.

两式相加，注意到 $OO' = 2OK$, $IO' = OI_a$ 化简就可以得出 $$ OI^2 + OI_a^2 = 2OK^2 + \frac{II_a^2}{2}$$.

令 $OI = d$, $OI_a = d_a$, $OO' = 2OK$，代入就可得式 $$d^2 + d_a^2 = 2R^2 + \frac{II_a^2}{2}$$

再利用已经证过的(\ref{eq:euler})(\ref{eq:another-euler})，得出要证明的公式：
$$ II_a^2 = 4R(r_a - r)$$

**参考文献**

A. Bogomolny, Euler's Formula and Poncelet Porism from Interactive Mathematics Miscellany and Puzzles
[http://www.cut-the-knot.org/triangle/EulerIO.shtml](http://www.cut-the-knot.org/triangle/EulerIO.shtml), Accessed 19 July 2013
