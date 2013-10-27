---
layout: post
title: "Git常用命令总结"
categories: develop
tags: [Git, Version Control]
description: |
  [Git](https://github.com/)是一个分布式版本控制软件, 网上有大量的介绍文章, 如[yulongfei的专栏](http://blog.csdn.net/gemmem/article/details/7290125), 这里仅对自己在使用过程中常用的命令总结一下.
---
{% include JB/setup %}

##个性化配置

首先是设置你的大名和邮箱:

{% highlight bash %}
$ git config --global user.name "Your Name Comes Here" 
$ git config --global user.email you@yourdomain.example.com 
{% endhighlight %}

设置喜欢的编辑器, 这里我用gedit. 注意一定要加上"-w", 意思是让git等待, 不然git是没有耐心等你把commit写完.

{% highlight bash %}
$ git config --global core.editor "gedit -w"
{% endhighlight %}

设置密码缓存, 默认缓存15分钟. 这样只需在第一次推送改变到远程仓库时输入github的用户名和密码, 后面就不用再输入了.

{% highlight bash %}
$ git config --global credential.helper cache
{% endhighlight %}

当然你可设置更长的时间, 如下面的3600秒.

{% highlight bash %}
$ git config --global credential.helper 'cache --timeout=3600'
{% endhighlight %}

##仓库地址管理

设置远程仓库地址:

{% highlight bash %}
$ git remote set-url origin https://github.com/weihuayi/weihuayi.github.io.git
{% endhighlight %}



