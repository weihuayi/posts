---
layout: post
title: "水平集方法"
categories: "numerical"
tags: [Level set,interface]
mathjax: true
description: |
  水平集方法是一种隐式描述移动界面的欧拉方法， 最早由 Osher 和 Sethian 在1988年引入。
---
{% include JB/setup %}

## 水平集方程的推导
在区域$\Omega$内，考虑随时间$t$演化的界面 $\Gamma = \Gamma({\bf x},t)$,
其中$\bf x$表示$\Gamma$上的一点。 移动界面可以用一个函数$\phi({\bf x},t)$
的零水平集表示, 即 $\Gamma = \{ {\bf x} | \phi({\bf x},t)=0 \}$。给定$\Omega$
上的速度向量场${\bf V}({\bf x},t)$, 则方程$\eqref{eq:lve0}$描述了$\phi$
的水平集以速度${\bf V}({\bf x},t)$在区域$\Omega$中传播的过程，该方程就称为**水平集方程**。 

$$
\begin{equation}
\phi_t + {\bf V}\cdot\nabla\phi=0 \label{eq:lve0}
\end{equation}
$$

$$
\begin{equation}\label{eq:lve1}
\frac{d}{dt}\phi(x(t),y(t),t)=0
\end{equation}
$$

$$
\begin{eqnarray}
\phi_t + \phi_x x_t + \phi_y y_t &=& 0 \label{eq:lva}\\
\phi_t + (x_t, y_t)\cdot(\phi_x,\phi_y) &=&0 \label{eq:lvb}\\
\phi_t + {\bf V}\cdot\nabla\phi &=& 0 \label{eq:lvc}
\end{eqnarray}
$$

其中${\bf V}= (x_t, y_t)$.

因为水平集$\phi(x,y,t)=c$的单位法向：

$$
\begin{equation}\label{eq:un}
{\bf n}(x,y,t)=\frac{\nabla\phi(x,y,t)}{\nabla\phi(x,y,t)}.
\end{equation}
$$

我们可以重写法向速度场为

$$
\begin{equation}\label{eq:nvf}
V_{\bf n}={\bf\rm V}(x,y,t)\cdot\frac{\nabla\phi(x,y,t)}{\nabla\phi(x,y,t)}.
\end{equation}
$$

$$
\begin{equation}\label{eq:lvf}
\phi_t + {\bf V}_{\bf\rm n}|\nabla\phi(x,y,t)|=0
\end{equation}
$$

{% referencelist %}
{% bibliography --file levelset %}

