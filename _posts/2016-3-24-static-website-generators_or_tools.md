---
layout: post
title: 11个最流行的静态(博客)网站生成工具
---

最近特别流行使用静态网站搭建博客，本博客就是host在GitHub Pages的静态网站。静态网站非常适合专注于内容的网站，例如，博客。那你可能会问，为什么不用大名顶顶的wordpress（动态网站）呢。

静态网站和动态网站相比有如下好处：

* 省钱。静态网站占用的系统资源少。如果挂到github pages上，只要注册一个域名就可以了。
* 速度快。不经过php解析器，不用数据库，速度自然比动态网站快
* 安全。由于静态网站的简洁，免疫很多web攻击方式。
* 服务器端配置简单。只需要一个web server（apache、nginx）。
* 非常容易维护。

静态网站的缺点是功能弱，和用户的交互能力不强。

********

静态网站生成工具能从简单的纯文本文件生成一个网站/博客。常用文本格式有reStructuredText和Markdown，我习惯使用Markdown。

如果你想搭建自己的静态网站，你可以选用下面列出的11个工具。

# Jekyll

[**Jekyll**](http://jekyllrb.com/)做为GitHub Pages的构建工具（Ruby语言），使它成为最流行的静态网站生成工具。Jekyll的流行也因为它非常简单，只需要基础的web开发基础。你可以使用它轻易的把文本转换为自定义的网站/博客。

如果你有wordpress或其他博客站点，你可以导入到Jekyll中。Jekyll支持插件、标签等等。

![Jekyll]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.14.06.png)

> Github Pages：<https://pages.github.com>
>
> 开始使用Jekyll：<http://jekyllrb.com/docs/quickstart/>

# Octopress

[**Octopress**](http://octopress.org/)是基于Jekyll的博客生成工具，它简化了Jekyll的操作，可以让你更舒服的创作。Octopress的一大优势是它插件很多，并且兼容Jekyll的官方插件。

Octopress支持内建的社交平台（Twitter, Google+），Disqus评论和Google Analytics。

![Octopress]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.15.31.png)

> Octopress的文档：<http://octopress.org/docs/>

# Hexo

[**Hexo**](https://hexo.io/)是用Node.js编写的博客框架。这个静态网站生成工具非常快，使用它构建一个完整的网站只需要几秒钟。Hexo支持所有的GitHub Markdown特性，并支持大多数Octopress插件。

从其他博客平台迁移到hexo非常容易。

![Hexo]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.17.21.png)

> [Hexo的文档]<https://hexo.io/docs/>

# Hugo

[Hugo]<http://gohugo.io/>是另一个流行的静态网站生成工具，它是使用go语言编写，并且使用Markdown语法。官网对它的描述：

> This application does not depend on administrative privileges, databases, interpreters, or external libraries, and still works like a charm. Websites or blogs built with Hugo can be hosted on any web host including GitHub Pages, S3, and Dropbox.

![Hugo]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.18.25.png)

> 开始使用Hugo：<http://gohugo.io/overview/quickstart/>

# Pelican

[**Pelican**](http://getpelican.com/)是使用Python编写的静态网站生成工具。它支持用reStructuredText, Markdown, 和AsciiDoc创作网站内容。Pelican支持Jinja模版引擎，结果是，它支持很多自定义主题。

![Pelican]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.22.50.png)

> 开始使用Pelican：<http://docs.getpelican.com/en/3.6.3/install.html>

# Middleman

[Middleman](https://middlemanapp.com/) －中间人，又一个使用Ruby编写的静态网站生成工具。它提供怎么使用和自定义的文档，方便你自定义你的网站。

> Middleman is a static site generator using all the shortcuts and tools in modern web development.

![Middleman]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.29.46.png)

> 开始使用Middleman：<https://middlemanapp.com/basics/install/>

# Metalsmith
[Metalsmith](http://www.metalsmith.io/)是简单、高效、pluggable静态网站生成工具，它使用nodejs编写。Metalsmith和其他工具的最大区别是它的所有东西都由插件处理，并且插件可以重用。只要决定网站的功能，然后找到相关插件，组合到一起，ok，ready to go!

Metalsmith也可以生成PDF、电子书、文档等等。

![Metalsmith]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 17.40.47.png)

> 开始使用Metalsmith：<http://www.metalsmith.io/>

# DocPad

[DocPad](http://docpad.org/)自带建立好的网站主架，允许你快速的建立功能完整的网站。这个工具支持CoffeeScript、Ruby、PHP、Stylus等等。

> DocPad removes limitations and closes the gap between experts and beginners. Designers and developers can create websites faster than ever before.

![DocPad]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 18.35.50.png)

> 开始使用DocPad：<http://docpad.org/docs/install>

# Wintersmith

[Wintersmith](http://wintersmith.io/)是极简的、可扩展的静态网站生成工具，它使用Nodejs编写。它同样支持插件。Wintersmith的项目基于目录结构，可以方便的移植旧站点。

![Wintersmith]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 18.47.45.png)

> 开始使用Wintersmith：<https://github.com/jnordberg/wintersmith#quick-start>

# Cactus

[Cactus](https://github.com/koenbok/Cactus/)是使用Python和Django模版系统制作的静态网站生成工具。

Cactus的源码托管在github：

![Cactus]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 18.59.32.png)

> 开始使用Cactus：<https://github.com/koenbok/Cactus/>

*******************

One more thing!

*******************

# HubPress

[HubPress](http://hubpress.io/)是开源的web应用，使用它可以允许你创建一个基于GitHub Pages的博客。HubPress的使用非常简单，你只需要fork这个项目到你的github，然后修改配置文件就可以了。

![HubPress]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-24 at 19.07.39.png)

> 开始使用HubPress：https://github.com/HubPress/hubpress.io

*****

不管你是创建单页面网站还是多页面网站，静态网站都是一个选择。

我这个博客使用Jekyll，托管在github pages。

而且使用markdown可以提升逼格－这篇博客就是使用vim写的，然后切换到命令行push一下代码，duang~。

当然，静态网站也有很多不足。