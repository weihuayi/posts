---
layout: post
title: "CGAL学习-三角化(3)"
categories: "CGAL"
tags: [triangulation, c++]
description: |
  Triangulation_2 是CGAL中描述二维三角形网格的一个类。基于CGAL进行二维三角形网格生成和优化算法开发，必须要掌握好这个类。
---
{% include JB/setup %}

## 介绍
Triangulation_2 是以"面-节点"的方式来表示一个三角形网格.

{% image cgal/rep_bis.png %}
Vertices and neighbors
{% endimage %}

## 例子
做下面的练习.

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
