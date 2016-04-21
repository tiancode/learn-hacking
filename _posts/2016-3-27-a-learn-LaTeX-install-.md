---
layout: post
title: LaTeX简要教程1:安装texlive
---

LaTeX编辑器有很多，你可以自由选择。你也可以使用在线编辑器 <http://overleaf.com/>。但是，为了教程的目的，我只使用Linux上的texlive软件包做为编译工具。

> LaTeX是一种基于TeX的排版系统，它能够在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

我使用的是Ubuntu系统。安装texlive，执行：

{% highlight shell %}
$ sudo apt-get install texlive
{% endhighlight %}

然后就可以用命令行工具pdflatex编译**.tex**文件，tex文件可以用任意文本编辑器创建，我使用vim。

> 如果你使用Windows，可以安装MiKTeX。
>
> 如果你使用Mac OS X，可以安装MacTeX。

### 测试LaTex：Hello World!

创建文件**hello.tex**：

{% highlight shell %}
$ vim hello.tex
{% endhighlight %}

写入如下内容：

{% highlight tex %}
\documentclass{article}

\begin{document}
    Hello World!
\end{document}
{% endhighlight %}

编译hello.tex：

{% highlight shell %}
$ pdflatex hello.tex
{% endhighlight %}

查看生成的pdf文档：

![Latex hello world]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 09.48.14.png)

*****

**问：pdflatex不支持中文，怎么办？**

安装texlive的完全体：

{% highlight shell %}
$ sudo apt-get install texlive-full
{% endhighlight %}

需要2G多硬盘空间。

代码：

{% highlight tex %}
\documentclass{article}
\usepackage{CJKutf8}

\begin{document}
\begin{CJK*}{UTF8}{gbsn}
    你好 死戒！   
\end{CJK*}
\end{document}
{% endhighlight %}

来自：http://tex.stackexchange.com/questions/107898/type-chinese-in-tex-compiled-with-latex