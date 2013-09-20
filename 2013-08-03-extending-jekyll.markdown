---
layout: post
title: 扩展 Jekyll 的功能
description: 给 Jekyll 扩展了 lesscss，参考文献，tikz 等功能。
categories: "Tools"
tags: ["Jekyll"]
---

最近发扬折腾精神，把博客从 ruhoh 上转换到了 jekyll 上。Jekyll 是 Github Pages 默认提供的工具，我曾经说过 jekyll 比 ruhoh 更原始，现在看来我错了。相比于 ruhoh，jekyll 更处于底层，但它的扩展性更强，ruhoh 虽然也可以扩展，但是它的用户少一些，相比之下，还是 jekyll 能找到的现成的 plugin 更多。当然，如果是刚刚用静态博客的生成器，还是推荐 ruhoh，它的文档写得可真的比 jekyll 的强得多啊，相比之下，jekyll 的文档连个像样的 get started 都没有。

Jekyll 和 ruhoh 两者都是基于 ruby 的实现，其基本思想都是差不多的：

每个文章都有 YAML 和 content。YAML 定义了一些变量，像文章的 layout，title，categories 等等。值得一提的是 layout 变量，指定这文章的布局。编译时，会去找 layout 指定的文件，把文章的 content，也就是内容插入到由 `{% raw %}{{ content }}{% endraw %}` 的位置中。

我扩展的第一个功能是 [Less css](http://lesscss.org) 功能。Less css 是个方便写 css 的工具，可以在写 less 时使用变量，函数，颜色运算等等好用的工具。

这个功能来自 [Github jekyll-less](https://github.com/zroger/jekyll-less)，把它的代码放入了我的 `_plugins/` 文件夹里。同时我也做了些定制，安装了 `yuicssmin` 这个压缩 css 文件的 gem 包。改动了点代码，在最终输出时把 css 文件压缩了下。
<!--more-->

{% highlight ruby %}
require 'less'
require 'yuicssmin' 

...

 FileUtils.mkdir_p(File.dirname(dest_path))
 begin
   content = File.read(path)
   content = ::Less::Parser.new({:paths => [File.dirname(path)]}).parse(content).to_css
   File.open(dest_path, 'w') do |f|
     f.write(Yuicssmin.compress(content)) # Add a Yuicompress tool
   end
...
{% endhighlight %}

另一个功能是用 `bibtex` 类型的文件实现参考文献的管理功能，正好有个方便的 [jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) 这样好用的工具，于是果断使用。

Jekyll-scholar 的一个比较高级的地方在它不但能处理参考文献，还能处理引用。像 `{% raw %}{% cite ruby %}{% endraw %}` 这样的代码就可以引用了。它是需要 csl 文件的，网上有个 [csl editor](http://editor.citationstyles.org) 很好用，可以根据自己的喜好定制。

最有挑战性的定制是处理 tikz 代码，网上并没有能用的工具，于是我就自己用 ruby 写了个 plugin。顺带说下为了写这个插件，我还看了 {% cite metaprogramming-ruby %} 这本书，真无奈～没点编程知识就是不行。

结论是，用这个代码：

{% highlight latex %}
{% raw %}
{% tikz ini %}
\draw (-1.5,0) -- (1.5,0);
\draw (0,-1.5) -- (0,1.5);
{% endtikz %}
{% endraw %}
{% endhighlight %}

会生成个 `ini.svg` 文件，同时返回它的引用，见图：

{% tikz ini %}
\draw (-1.5,0) -- (1.5,0);
\draw (0,-1.5) -- (0,1.5);
{% endtikz %}

这个插件的代码太长了，有兴趣可以看看它的 [Gist](https://gist.github.com/Maxfan-zone/6139753)。

参考文献

{% bibliography --cited %}
