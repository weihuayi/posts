---
layout: post
title: 复数基础续集
date: '2013-09-15'
description: De Moivre 公式，Euler 公式和一些有趣的复数的结果。
categories: "Analysis"
tags: [Complex number, Euler's formula, De Moivre's formula, Trigonometric]
mathjax: true
---

两个复数之间的乘法，有一个几何解释是把它们的幅角相加而模相乘。对于复数 $z = \rho(\cos\varphi + i \sin\varphi)$ 和它本身相乘，我们可以得到：

$$ z ^ 2 = \rho^2 (\cos 2\varphi + i \sin 2\varphi) $$

再用 $z$ 乘这个公式：

$$ z ^ 3 = \rho^3 (\cos 3\varphi + i \sin 3\varphi) $$

就这样一直乘下去：

$$ z ^ n = \rho^n (\cos n\varphi + i \sin n\varphi) $$

特别地，我们让 $z$ 为单位圆上的点，即 $\rho = 1$。这样我们就得到：

$$ z ^ n = (\cos n\varphi + i \sin n\varphi) $$

把 $ z = \cos\varphi + i \sin\varphi $ 代入，就可以得到：

$$ (\cos\varphi + i \sin\varphi)^n = (\cos n\varphi + i \sin n\varphi) $$

这就是复数中特别重要的 De Moivre 公式。

定义一个函数 $E(\varphi) = \cos\varphi + i \sin\varphi $ 表示幅角为 $\varphi$ 的单位圆上的复数，则我们就把 De Moivre 公式化简为 $[E(z)]^n = E(nz)$。

函数 $E(\varphi)$ 有几个重要的性质需要说明。首先地，有 $E(\varphi_1) \cdot E(\varphi_2) = E(\varphi_1 + \varphi_2)$，这是复数相乘的直接推论，两个复数相乘，模都是 $1$，而幅角要相加。其次，我们还有 $E(\varphi_1) / E(\varphi_2) = E(\varphi_1 - \varphi_2)$，即复数相除，模相除，幅角相减。

De Moivre 公式可以用来解这样一个问题：

{% problem %}
求 $\sum_{k = 1}^{n}\sin(kx)$ 和 $\sum_{k = 1}^{n}\cos(kx)$。
{% endproblem %}

<!--more-->

{% solution %}
我们知道

$$
\begin{equation}
\label{eq:1}
\sum_{k = 1}^{n} E(k \varphi) = \sum_{k = 1}^{n}\cos(kx) + i\sum_{k = 1}^{n}\sin(kx)
\end{equation}
$$

且

$$
\begin{equation}
\label{eq:2}
\sum_{k = 1}^{n} E(k \varphi) = \sum_{k = 1}^{n} [E(\varphi)]^k
\end{equation}
$$

由等比级数公式

$$
\begin{eqnarray*}
\sum_{k = 1}^{n} [E(\varphi)]^k &=& \frac{E(\varphi) - [E(\varphi)]^{n+1}}{1 - E(\varphi)}\\
                                &=& \frac{E(\varphi) - E[(n+1)\varphi]}{1 - E(\varphi)}
\end{eqnarray*}
$$

利用三角函数半角公式

$$
\begin{eqnarray*}
1 - E(\varphi) &=& 1 - \cos\varphi - i\sin\varphi \\
               &=& 2\sin^2\frac{\varphi}{2} - 2i\sin\frac{\varphi}{2}\cos\frac{\varphi}{2} \\
               &=& 2\sin\frac{\varphi}{2} \cdot [-i(\cos\frac{\varphi}{2} + i\sin\frac{\varphi}{2}] \\
               &=& -2i\sin\frac{\varphi}{2}E(\frac{\varphi}{2})
\end{eqnarray*}
$$

所以由函数 $E(\varphi_1)/E(\varphi_2) = E(\varphi_1 - \varphi_2)$ 的这个性质，就能得到

$$
\begin{eqnarray}
\sum_{k = 1}^{n} [E(\varphi)]^k &=& \frac{E(\varphi) - E[(n+1)\varphi]}{1 - E(\varphi)}\nonumber \\
                                &=& \frac{E(\varphi) - E[(n+1)\varphi]}{-2i\sin\frac{\varphi}{2}E(\frac{\varphi}{2})}\nonumber \\
                                &=& \frac{E(\frac{\varphi}{2}) - E[(n+\frac{1}{2})\varphi]}{-2i\sin\frac{\varphi}{2}}\nonumber \\
                                &=& \frac{iE(\frac{\varphi}{2}) - iE[(n+\frac{1}{2})\varphi]}{2\sin\frac{\varphi}{2}}\label{eq:3} \\
\end{eqnarray}
$$

我们把分子化简：

$$
\begin{eqnarray}
iE(\frac{\varphi}{2}) - iE[(n+\frac{1}{2})\varphi] &=& \sin(n+\frac{1}{2})\varphi - \sin\frac{\varphi}{2} \nonumber \\ 
&&+ i[\cos\frac{\varphi}{2} - \cos(n + \frac{1}{2})\varphi] \label{eq:4}
\end{eqnarray}
$$

这样，由 ($\ref{eq:1}$)($\ref{eq:2}$)($\ref{eq:3}$)($\ref{eq:4}$) 化简后，实部与虚部对应，就能得到

$$
\begin{eqnarray*}
\sum_{k = 1}^{n}\sin(kx) &=& \frac{\cos\frac{\varphi}{2} - \cos(n + \frac{1}{2})\varphi}{2\sin\frac{\varphi}{2}} \\
\sum_{k = 1}^{n}\cos(kx) &=& \frac{\sin(n+\frac{1}{2})\varphi - \sin\frac{\varphi}{2}}{2\sin\frac{\varphi}{2}}
\end{eqnarray*}
$$
{% endsolution %}

把 $E(\varphi)$ 的性质与指数函数 $e^x$ 相对比。我们有 $e^{x_1} \cdot e^{x_2} = e^{x_1 + x_2}$ 和 $e^{x_1} / e^{x_2} = e^{x_1 - x_2}$。

我们在两个函数上看到了惊人的相似性。事实上，Euler 公式 $e^{ix} = E(x)$ 揭示了它们之中的联系。

{% prove %}
这个公式的证明要从 $(\cos n\varphi + i \sin n\varphi) = (\cos\varphi + i\sin\varphi)^n$ 开始，我们代入 $x = n\varphi$ 即 $\varphi = \frac{x}{n}$，得到：

$$(\cos x + i \sin x) = (\cos\frac{x}{n} + i \sin\frac{x}{n})^n$$

现在如果 $x$ 是一个定值，根据现代的极限理论，我们有

$$ 
  \lim_{n \to \infty} \cos\frac{x}{n} = 1
$$

且有对任意一个 $x$ 都有 $$\lim_{n\to\infty} \frac{\sin\frac{x}{n}}{\frac{x}{n}} = 1$$

于是我们就有了这样一个看起来合理的公式：

$$\cos x + i \sin x = \lim_{n \to \infty} (1 + \frac{x}{n})^n$$

把它与 $e^x$ 的定义

$$ e^x = \lim_{n \to \infty} (1 + \frac{z}{n})^n$$

对比，就能看出

$$
\begin{equation}
\label{eq:euler}
\cos x + i \sin x = e^{ix}
\end{equation}
$$

就是 $E(x) = e^{ix}$
{% endprove %}

{% property %}
三角函数与双曲函数有这样的联系：

$$
\begin{eqnarray*}
\cos(iy) &=& \cosh y \\
\sin(iy) &=& i\sinh y
\end{eqnarray*}
$$
{% endproperty %}

{% prove %}
根据 Euler 公式，我们把 $-x$ 代入，得

$$
\begin{equation}
\label{eq:neuler}
\cos x + -i \sin x = e^{-ix}
\end{equation}
$$

由 ($\ref{eq:euler}$) 和 ($\ref{eq:neuler}$) 相加与相减，就能得到：

$$
\begin{eqnarray}
\label{eq:cos}
2\cos x &=& \frac{e^{ix} + e^{-ix}}{2} \\
\label{eq:sin}
2\sin x &=& \frac{e^{ix} - e^{-ix}}{2}
\end{eqnarray}
$$

这两个公式也被认为是 Euler 公式。

把复数 $x = iy$ 代入，能得到这么有趣的东西：

$$
\begin{eqnarray*}
\cos(iy) &=& \frac{e^{x} + e^{-x}}{2} \\
         &=& \cosh y \\
\sin(iy) &=& \frac{e^{-x} - e^{x}}{2i} \\
         &=& i\frac{e^{x} - e^{-x}}{2} \\
         &=& i\sinh y
\end{eqnarray*}
$$
{% endprove %}
{% referencelist %}
{% bibliography --file complex-number-theory.bib %}
