---
layout: post
title: LaTeX简要教程7:生成目录
---

LaTeX提供了自动生成目录的命令，非常简单直接。

LaTeX使用section、subsection等命令创建标题/段落，目录根据这些标题生成。

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-30 at 10.04.08.png)

简单例子：

{% highlight tex %}
\documentclass{article}

\begin{document}

\tableofcontents
\newpage

\section{First Section}

some text

\subsection{First Sub Section}

some text

\end{document}
{% endhighlight %}

编译.tex文件两次，你会得到如下目录：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-30 at 10.22.44.png)

同样可以为表格和图像生成目录列表；使用\listoffigures和\listoftables命令：

{% highlight tex %}
\begin{figure}
  %...
  \caption{picture}
  %...
\end{figure}

\begin{table}
  %...
  \caption{table}
  %...
\end{table}
...
\begin{appendix}
  %...
  \listoffigures
  \listoftables
  %...
\end{appendix}
{% endhighlight %}

总结：

* 使用\tableofcontents命令生成目录
* 需要编译.tex文件两次
* 使用\listoffigures和\listoftables命令为表格和图像生成目录