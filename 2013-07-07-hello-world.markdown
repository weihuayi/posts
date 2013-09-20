---
layout: post
title: Hello, world!
date: '2013-07-07'
description: 使用 Godaddy 和 Github Pages 建起网站的经验记录。
categories: "Misc"
tags: [Web]
---

我自己早就想弄一个博客了，但是一直条件受限制。一是中考之前没有时间，现在中考之后终于有了时间;二是国内的博客服务都不好，我都不满意，国外的博客服务 Blogger, Wordpress 访问在中国大陆受限，最终我决定自己找空间。于是我就开始搭建我的博客。


先解决的是空间，因为缺钱，最好可以用免费又访问快的服务。于是乎，我用了 [GitHub](http://github.com) 的 User Page 服务，完全免费。不过这也让我学习了 git 这个版本控制系统，推荐看 [Pro Git](http://git-scm.com/book)，但貌似要跨栏。关于 [Github Pages](http://help.github.com/categories/20/articles) 的帮助写得也很详尽，我就不多言了。

<!--more-->
不过，我在创建 ssh 连接，让 git 的 push 操作不用输入用户名和密码时，还是遇到了困难。[GitHub](https://help.github.com/articles/generating-ssh-keys) 上的说明似乎缺了一步。在设置完成后，要把在仓库的`.git/config`文件中的`url`选项改成：

    url = git@github.com:USERNAME/REPONAME.git

域名注册是在 Godaddy.com，注册域名不用备案的`^_^`。这个域名提供商的最大好处就是可以用支付宝(Alipay)， Arch linux 需要安装 AUR 源中的`aliedit`插件（嘿嘿，支付宝这东西 Linux 也能用）。虽然我没有手机，只能用老妈的支付宝账号，但我还是觉得它挺方便的。

博客选用了 Static Blog，Jekyll 这货是 GitHub 默认提供的工具，不过它相比 Ruhoh 也显得太原始了。Ruhoh 我还在研究中，以后再更新吧。
