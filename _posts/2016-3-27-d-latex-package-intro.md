---
layout: post
title: LaTeX简要教程4:包(package)－添加更多功能
---

LaTeX默认提供了很多命令，但是有时并不能满足需要，这时就要引入包里面的功能。下面使用equation、amsmath包做例子，它们都可以实现基本的数学公式排版。

使用**\usepackage**命令导入包，注意这个命令使用的位置：

{% highlight tex %}
\documentclass{article}

\usepackage{Package Name}

\begin{document}
...
...
\end{document}
{% endhighlight %}

### 怎么安装包

如果你使用的是Linux，那么大多数包已经默认安装了。可以执行如下命令安装可用的所有LaTeX包（Ubuntu）：

{% highlight shell %}
$ sudo apt-get install texlive-full
{% endhighlight %}

如果你使用的是MiKTeX（Windows），它会下载你引入的包。

### 使用包

LaTeX有很多很多包，提供各种各样的功能。我会介绍一些常用的包。

LaTeX提供了一个叫equation的“环境”，它可以实现数学公式排版。在begin{equation}和\end{equation}之间的代码会使用"数学模式"，例如：

{% highlight tex %}
\documentclass{article}

\begin{document}

\begin{equation}
   f(x) = x^2
\end{equation}

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 17.28.10.png)

上面代码在数学公式后加了一个编号，这个编号是默认自动生成的，它不能移除。但是你可以使用amsmath包把它移除，代码如下：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{equation*}
  f(x) = x^2
\end{equation*}

\end{document}
{% endhighlight %}

现在我们得到了和前面一样的输出，只是数字被移除了：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 19.52.42.png)

*******

包还可以提供图像、链接和参考文献等等功能。