---
layout: post
title: LaTeX简要教程2:第一个基于LaTeX的文档
---

在这篇教程中，我们创建几个基本的LaTeX文档，并对LaTeX语法进行解释。

### 基本的LaTeX文件结构

使用LaTeX创建文档是很简单的，它和**MS Word**的不同是，你书写的是包含LaTeX代码和实际内容的纯文本文件（.tex文件）。LaTeX代码控制实际内容的格式/样式。在编译时.tex文件会转换成.pdf文档，例如教程1里的代码：

{% highlight tex %}
\documentclass{article}

\begin{document}
    Hello World!
\end{document}
{% endhighlight %}

编译之后，生成的PDF文档中会有**Hello World!**字样，文档底部的页码也是自动生成的。

让我们来解析一下上面的代码。你可以看到有许多以\开头的语句，这些语句并不是实际的内容，它是LaTeX命令。所有命令都是这种结构：**\command{option}**。command是命令的名字，大括号里的option指定命令使用的参数。

\documentclass{article}：设置文档的种类，这影响文档的基本格式。如果你使用book，它的样式和article是不一样的。

\begin，\end语句：这其实并不是命令，而是定义了环境。begin和end间的环境代表这块区间应用的排版规则。在文档中可以有多个环境，下面代码展示环境的使用方法：

{% highlight tex %}
% 正确用法:

\begin{document}
  \begin{environment1}
    \begin{environment2}
    \end{environment2}
  \end{environment1}
\end{document}

% 错误用法:

\begin{document}
  \begin{environment1}
    \begin{environment2}
  \end{environment1}
    \end{environment2}
\end{document}
{% endhighlight %}

% 开头的代码是注释。

### 丰富页面

当你的文档中使用数学公式或图表时，你会使用到更多的环境。当然，你也可以自定义环境。LaTeX自带了常用的环境，这些环境使用包（package）引入，后面教程会有说明。

添加更多命令使文档内容更丰富：

{% highlight tex %}
\documentclass{article}

\title{Hello you}
\date{2015-09-01}
\author{olly shit}

\begin{document}
  \maketitle
  \newpage

  Hello World!
\end{document}
{% endhighlight %}

\title、\date和\author并没有在document环境中，所以它们并不会在文档中显示。

\maketitle自动创建“扉页”；\newpage创建新页面。

上面代码生成了两页文档，如下：

第一页：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 11.52.56.png)

第二页：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 11.53.06.png)

注意，上面创建的文档在扉页上有页码，这不符合文档格式。

我们可以移除第一页的页码，代码如下：

{% highlight tex %}
\documentclass{article}

\title{Hello you}
\date{2015-09-01}
\author{olly shit}

\begin{document}
  \pagenumbering{gobble}
  \maketitle
  \newpage
  \pagenumbering{arabic}

  Hello World!
\end{document}
{% endhighlight %}

页码将从第二页文档开始，起始值是数字1。

关于pagenumbering命令的选项：

* gobble：没有页码
* arabic：阿拉伯数字
* roman：罗马数字