---
layout: post
title: "CGAL学习-安装 (1)"
categories: "CGAL"
tags: [install, cmake]
description: |
  CGAL是一个C++编写的开源计算几何算法库。它的目标是以C++库的形式提供易用、高效和可靠的计算几何算法。
---
{% include JB/setup %}

## CGAL介绍
[CGAL](http://www.cgal.org/)（Computational Geometry Algorithms Library）是一个
大型的C++开源计算几何算法库, 它的目标是以C++库的形式提供易用、高效和可靠的计算几何算法。 

CGAL提供了很多常用的几何数据结构和算法，如三角化（Triangulations）、Voronoi 图（Voronoi diagrams）、多边形和多面体布尔操作（Boolean operations on polygons and on polyhedra）、网格生成（ mesh generation ） 、几何处理（geometry processing）等。

这些数据结构和算法的基础是基本的几何对象及对这些基本几何对象的操作, 这些基本的几何对象和操作封装在几何核心(Geometry Kernel) 类中。

基本的几何对象，如：

* 点
* 线段
* 直线
* 三角形
* 圆
* ......


基本的几何操作，如：

* 获取坐标
* 计算长度
* 计算面积
* 计算相对位置关系
* ......

另外, CGAL还提供了一些支持库(SupporT Library), 提供几何对象生成器(geometric object generators)
和空间排序函数(spatial sorting functions), 以及第三方的软件接口如QT和Geoview等.

## CGAL 安装
这里仅介绍Ubuntu中的安装方法, 其它操作系统的安装以后会陆续介绍.

首先从Ubuntu自带的软件源中, 安装下列软件:
{% highlight bash %}
$sudo apt-get install g++ gcc #编译器
$ sudo apt-get install gdb #调试器
$ sudo apt-get install cmake-qt-gui cmake # 软件构建系统 
# QT相关的软件, 其中qtcreator是一个类似于VC++图形编程环境
$ sudo apt-get install qtcreator qt4-dev-tools qt4-doc qt4-qtconfig qt4-demos qt4-designer
$ sudo apt-get install libgmp-dev libmpfr-dev
$ sudo apt-get install geomview
$ sudo apt-get install libqglviewer-dev
{% endhighlight %}

下载[Boost](http://www.boost.org/users/download/), 进入解压目录:
{% highlight bash %}
$ ./bootstrap.sh
$ ./bjam --prefix=/usr/local/ #安装目录是/usr/local/
$ sudo ./bjam install
{% endhighlight %}

下载并行矩阵计算软件包[Eigen](http://bitbucket.org/eigen/eigen/get/3.2.0.zip), 进入解压目录:
{% highlight bash %}
$ mkdir build
$ cd build
$ cmake ../
$ sudo make install  
{% endhighlight %}

下面就可以安装CGAL啦. 首先下载最新[CGAL](https://gforge.inria.fr/frs/?group_id=52&release_id=7462), 进入解压目录:
{% highlight bash %}
$ cmake .
$ make
$ sudo make install
{% endhighlight %}

在学习CGAL的时候，要涉及很多知识和工具，但要学会突出重点，有些需要深入理解和掌握，
但有些工具只需要学会使用即可，如下面的CMake。
## CMake
如[CMake](http://www.cmake.org/)， 它是一个跨平台开源软件构建系统, CGAL就是利用它构建的。 
基本用法见中文手册[CMake 实践](http://sewm.pku.edu.cn/src/paradise/reference/CMake%20Practice.pdf)

用CMake构建你自己编写的CGAL程序时，要读取一个命为CMakeLists.txt文件，这个文件主要包含下面三方面信息：

1. 头文件及其所在目录信息
2. 源文件及其所在目录信息
3. 库文件及其所在目录信息

下面给出一个简单的CMakeLists.txt的例子。

{% highlight bash %}
#设置工程名字, 可以换成你喜欢的名字
project( project_name )
#设置CMake的版本要求
cmake_minimum_required(VERSION 2.6.2) 
#设置一个变量SRC, 变量值就是后面源文件和头文件的名字， 你可以换成你的源文件和头文件的名字
set(SRC main.cpp header1.h header2.h header3.h )
#查找CGAL的头文件和库文件
find_package(CGAL QUIET COMPONENTS Core ) 
if ( CGAL_FOUND ) #如果找到CGAL
  include( ${CGAL_USE_FILE} ) 
  include( CGAL_CreateSingleSourceCGALProgram )
  create_single_source_cgal_program(${SRC})
else() # 找不到时输出错误信息
    message(STATUS "This program requires the CGAL library, and will not be compiled.")
endif()
{% endhighlight %}

CMake读取CMakeLists.txt文件，会根据你系统配置生成相应的Makefile文件，然后你就可以利
用make命令编译出你的可执行程序了， 命令如下：

{% highlight bash %}
$ cmake .
$ make
{% endhighlight %}







