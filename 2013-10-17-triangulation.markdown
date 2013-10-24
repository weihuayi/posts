---
layout: post
title: "CGAL学习-三角剖分(3)"
categories: "CGAL"
tags: [triangulation, c++]
mathjax: true
description: |
  Triangulation_2 &lt Traits,TDS &gt 是CGAL中描述二维三角形剖分的一个模板类。实例化时, 它的第一个模板参数要传入一个几何核心类, 第二个模板参数是一个三角剖分的数据结构类（这个参数有一个默认的值）。这个模板类定义了三角剖分的基本用户接口， 它也是其它三角剖分类（如Delaunay_triangulation_2、Regular_triangulation_2）的基类。 因此它是基于CGAL进行二维三角形网格生成和优化算法开发，必须要掌握好这个类。
---
{% include JB/setup %}

## 介绍
Triangulation_2\<Traits,TDS\> 中存储了一个二维三角形网格的所有节点(vertex)和所有三角形面(face)。为了算法处理上的便利
，这个类引入了一个“无限”节点， 它不含坐标信息。这个无限点和三角形网格边界上的节点又构成了无限边和无限面，这样三角形
网格中的所有边都被两个面共有（每条边界边被一个有限面和一个无限面共有）, 见下图。

{% image cgal/infinite.png %}
Infinite vertex and infinite faces.
{% endimage %}

Triangulation_2\<Traits,TDS\> 中，除了无限节点外，所有的节点都包含坐标信息、所属的某个三角形面信息。每个三角形面都包
含了三个顶点的信息和三个邻居三角形面信息。在一个三角形面中， 三个顶点的局部编号为0、1和2，方向为逆时针方向。三个邻居
三角形面的编号规则是：$i$号顶点对应$i$号邻居，见下图。

{% image cgal/rep_bis.png %}
Vertices and neighbors.
{% endimage %}

Triangulation_2\<Traits,TDS\>　中对节点和三角形面的访问是通过 handle、iterator 和 circulator, 它们的用法和指针类似，
通过"->"来访问其成员函数，但比单纯的指针用起来更安全（单纯的指针如果忘记初始化就使用，后果就很严重）。下面给出一个
Vertex_handle 类型的变量的基本用法：

{% highlight cpp %}
Vertex_handle vh ...;
Point_2 p = vh->point(); //访问其坐标信息，返回一个 Poing_2 类。
vh->set_point(p); //设定其坐标信息。
{% endhighlight %}

下面是　Face_handle 类型的变量的基本用法：

{% highlight cpp %}
Face_handle fh ...;
int i = 0;
Vertex_handle vh = fh->vertex(i);
Face_handle fhi = fh->neighbor(i);
Face_handle fhj = fh->neighbor(fh->ccw(i));
Face_hanele fhk = fh->neighbor(fh->cw(i));
{% endhighlight %}

Triangulation_2\<Traits,TDS\>中，边是这样定义如下：

{% highlight cpp %}
typedef std::pair<Face_handle,int> Edge;
Edge e；// e.first 的类型是 Face_handle, 存储边 e 所属的一个三角形面；
       // e.second 的类型是 int， 存储边 e 在 e.first　中的局部编号。
       // 三角形面中边的局部编号规则是：$i$号顶点对应$i$号边。
{% endhighlight %}

在Triangulation_2\<Traits,TDS\> 中，要遍历所有的节点、边或三角形面，要用到相应的 iterator，　如：

* Finite_faces_iterator
* Finite_edges_iterator
* Finite_vertices_iterator

要遍历一个节点周围的节点、边或单元，要用到 circulator，　如：

* Face_circulator
* Edge_circulator
* Vertex_circulator

## 例子
完善下面的代码，练习使用　Triangulation_2\<Traits,TDS\>　的接口。

{% highlight cpp %}
#include <fstream>
#include <unistd.h> // for sleep()

#include <CGAL/Exact_predicates_inexact_constructions_kernel.h>
#include <CGAL/Triangulation_vertex_base_2.h>
#include <CGAL/Triangulation_face_base_2.h>
#include <CGAL/Triangulation_data_structure_2.h>
#include <CGAL/Triangulation_2.h>
#include <CGAL/Delaunay_triangulation_2.h>

#include <CGAL/IO/Geomview_stream.h>
#include <CGAL/IO/Triangulation_geomview_ostream_2.h>
#include <CGAL/Bbox_3.h>


typedef CGAL::Exact_predicates_inexact_constructions_kernel K;

typedef CGAL::Triangulation_vertex_base_2<K> vb;
typedef CGAL::Triangulation_face_base_2<K> fb;
typedef CGAL::Triangulation_data_structure_2<vb,fb> Tds;
typedef CGAL::Triangulation_2<K,Tds>  Triangulation_2;

typedef Triangulation_2::Vertex_handle Vh;
typedef Triangulation_2::Face_handle Fh;

typedef Triangulation_2::Finite_vertices_iterator Fvi;
typedef Triangulation_2::Finite_faces_iterator Ffi;
typedef Triangulation_2::Finite_edges_iterator Fei;
typedef Triangulation_2::Edge Edge;


typedef K::Point_2 Point_2;

//在这里定义需要的类型, 实现下面要求的代码.


int main()
{
    Triangulation_2 tri;

    // 插入一组点
    std::vector<Point_2> pts(4);
    pts[0]=Point_2(0.0,0.0);
    pts[1]=Point_2(1.0,0.0);
    pts[2]=Point_2(1.0,1.0);
    pts[3]=Point_2(0.0,1.0);

    tri.insert(pts.begin(),pts.end());

    std::cout<<tri.number_of_faces()<<std::endl;
    std::cout<<tri.number_of_vertices()<<std::endl;

    //显示三角形网格
    CGAL::Geomview_stream gv(CGAL::Bbox_3(0,0,-0.001,1,1,0.001));
    gv.set_wired(true);
    gv.set_line_width(1);
    gv.set_bg_color(CGAL::Color(0, 200, 200));
    gv << tri;
    sleep(10);


    //遍历所有的边, 计算每个边的中点, 并插入到网格中

    //遍历所有的单元, 计算每个单元的质心, 并插入到网格中

    for(int i = 0; i < 10; i++)
    {
        //遍历所有的节点，利用其周围的节点的平均更新该节点的坐标

    }

    //遍历所有的边, 如果是内部边, 且共用它的两个三角形中和这个边相对的两个角度之和大于180度,
    //做换边操作
    // tri.flip(Face_handle f, int i)

    return 0;
}
{% endhighlight %}
