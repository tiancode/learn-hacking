---
layout: post
title: LaTeX简要教程6:添加图像/图片
---

这篇教程教你怎么使用LaTeX在文档中嵌入图像。需要使用graphicx包。

例子：

{% highlight tex %}
\documentclass{article}

\usepackage{graphicx}

\begin{document}

\begin{figure}
  \includegraphics[width=\linewidth]{dirty.jpg}
  \caption{something beauty.}
  \label{fig:dirty}
\end{figure}

Picture \ref{fig:dirty} is shot in north

\end{document}
{% endhighlight %}

_注意：替换图片文件路径。我把图片放到了.tex文件所在目录。_

生成的pdf如下图：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-30 at 09.28.39.png)

figure环境会处理图片在文档中的位置和数字标识。导入图像，使用**\includegraphics**命令，参数为图像文件的路径；还有一个参数是 `width=\linewidth` ，指定把图像缩放以适应文档的宽度。

\caption命令设置图像下的标题。\label在文档中不可见的，文档中其他地方可以通过这个引用。

### 强制图像在特定位置显示

在以后你会注意到，在代码中添加图像的位置和生成的图像位置不一定对应。如果你的文档包含大量文本，LaTeX也许会把图像放到下一页，或其他有充足空间的地方。可以通过如下代码强制图像在特定位置显示：

{% highlight tex %}
\begin{figure}[h!]
。。。
\end{figure}
{% endhighlight %}

\begin后的**h!**代表在文档当前位置显示，可能的值如下：

* h(here)：
* t(top)：页头
* b(bottom)：页底
* p(page)：
* !(override) 

总结：

* 使用graphicx包和figure环境嵌入图像
* 图像会自动编号
* 添加h!]设置图像位置