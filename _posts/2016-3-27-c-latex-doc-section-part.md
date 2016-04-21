---
layout: post
title: LaTeX简要教程3:添加段落和章节
---

在上一篇教程中，我们创建了一个基本的文档，本文将为文档添加段落和章节。为了实现它，使用LaTeX提供的段落标题命令：

{% highlight tex %}
\section{}
\subsection{}
\subsubsection{}

\paragraph{}
\subparagraph{}
{% endhighlight %}

**示例：标题和子标题**

在上一个教程的基础上添加：

{% highlight tex %}
\documentclass{article}

\begin{document}

  \section{Hello}

    Hello World!

    \subsection{Sub Hello}

      Hello M!

\end{document}
{% endhighlight %}

标题会自动添加数字编码，效果如下：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 16.13.11.png)

第二个例子：

{% highlight tex %}
\documentclass{article}

\begin{document}

\section{Hello}

  Hello World!

  \subsection{Sub Hello}

    Hello Earth!

    \subsubsection{Sub Sub Hello}

      Hello Me!

      \paragraph{Paragraph}

        babalalala

        \subparagraph{Sub Paragraph}

          more balabalabala

\section{World}

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-27 at 16.23.29.png)

使用LaTeX组织文档结构非常简单，很多人使用"MS Word"都做不好。

总结：

* LaTeX创建段落的命令：**\section、\subsection、\subsubsection**
* section段落标题前使用连续的数字做为章节号，并出现在目录中
* paragraph不使用数字标示，也不会出现在目录中

在下一节的教程中，我简单介绍一下package（包），并为数学公式排版，这也是LaTeX突出的地方。