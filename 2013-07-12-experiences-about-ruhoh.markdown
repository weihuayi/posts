---
layout: post
title: Ruhoh 小结
date: '2013-07-12'
description: 使用 ruhoh 的记录。
categories: "Tools"
tags: [ruhoh, web]
---

最近在折腾 ruhoh，放下了所有的正事，包括基础物理学，数学与猜想什么的，集中起精力来做这件事，由于我坑爹的英文水平，加上我的挖掘癖好，不论是什么代码都要搞明白不可，我的进展就像蜗牛一样慢，但这也教会了我要有耐心，不过几天以后，总结起来还是有收获的。

我把 ruhoh 上传到了 Github 上，方便自己的管理和他人研究。（EDIT: 现已废弃。）

说实话，ruhoh 最强大的功能就是 widgets，几乎不论什么 HTML 代码，只要在`widgets`文件夹中定义一个，就能方便地管理。例如，我在`widgets/mathjax`中定义了 MathJax 插件，把 MathJax 的代码输入进去：
<!--more-->

{% highlight html %}
<!-- MathJax -->
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">                                                                                           
</script>
<!-- End MathJax -->
{% endhighlight %}

然后在`config.yml`中定义 MathJax widget:

{% highlight yaml %}
mathjax :
  use : mathjax
  enable : true
{% endhighlight %}

注意缩进！我可吃了不少苦头。使用 MathJax 的方法是在需要的地方（`twitter/layouts/default.html`里）插入`{% raw %}
{{ widgets.mathjax }}
{% endraw %}`就可以使用 MathJax 了。

曾经有人提到过给它加个开关的功能，其实是可以做到的，在不需要它的时候，可以在 [YAML Metadate](http://ruhoh.com/docs/2/pages/#toc_6) 这一节中加上 Per-page disable：

{% highlight yaml %}
widgets:
  mathjax:
    enable: false
{% endhighlight %}

[官方文档](http://ruhoh.com/docs/2/widgets/comments/)有提到过，但不是用在 MathJax 上的。

另请各位大侠猜一猜`{% raw %}
{{ widgets.mathjax }}
{% endraw %}`是怎么逃过 mustache 的转换的？`^_^`

本博客的[存档](/archive)页面我可做了点定制（很多人都没发现`-_-;`），在`_root/archive.html`中，文件的内容中有

{% highlight django %}
{% raw %}
{{# posts.collated }}
  {{> posts_collate }}
{{/ posts.collated }}
{% endraw %}
{% endhighlight %}

这么几行，果然找到了`{% raw %}
{{> posts_collate }}
{% endraw %}`
的[定义](https://github.com/ruhoh/ruhoh.rb/blob/master/system/partials/posts_collate.html)。经过一番篡改，`_root/archive.html`变成了这般模样：

{% highlight html %}
{% raw %}
{{# posts.collated }}
{{#months}}
  <div id="blog-archives">
    <h2>{{ year }}</h2>
    {{#posts?to_posts}} 
      <article>
        <h1><a href="{{ url }}">{{title}}</a></h1>
        <time>{{ date }}</time>
        <footer>
        <span class="categories">
          分类
          {{#categories}}
          <a href="{{url}}">{{ name }}</a>
          {{/categories}}
          标签
          {{#tags}}
          <a href="{{ url }}">{{ name }}</a>
            {{/ tags}}
        </span>
        <p>{{ description }}<p>
        </footer>
      </article>
      {{/posts?to_posts}}
</div>
{{/months}}
{{/ posts.collated }}
{% endraw %}
{% endhighlight %}

再加上 CSS 文件的辅助，我的存档页面就与 [Pluskid](http://freemind.pluskid.org/archive) 的风格相似。

我用 ruhoh 最不顺心的地方就是 markdown 语言的过分简单，最不可忍受的就是参考文献系统，为什么就不能像 bibtex 一样方便地在一个文件中管理参考文献呢？于是我决定转用 pandoc，把 latex 生成 HTML。解决方案挺复杂的，还要做 csl 定制，目前还没有完成。

我还要谈的就是本博客的主题。因为我不会写 CSS 代码，于是就抄袭和修改了其它网站的源码，虽说我对现在的主题并不满意（怪我自己），但是也要对 [Disqus](http://disqus.com)、[Pluskid](http://freemind.pluskid.org)、[DandyWeng](http://dandyweng.com)和 Twitter 的开放源码的 [Bootstrap](http://twitter.github.io/bootstrap) 表示感谢，同时感谢 [Joseph Pan](http://hahack.com) 的支持。

**参考文献**

[Ruhoh 官方文档](http://ruhoh.com/docs/2/)

[From WordPress to Ruhoh](http://hahack.com/tools/from-wordpress-to-ruhoh)

[Ruhoh 札记](http://dourok.info/2012/08/20/something-about-ruhoh/)

[The Unbearable Madness of Static Blog Generators](http://freemind.pluskid.org/technology/the-unbearable-madness-of-static-blog-generators/)
