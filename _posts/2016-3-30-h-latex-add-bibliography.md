---
layout: post
title: LaTeX简要教程8:添加表格
---

有时候，需要在文档中插入表格。LaTeX提供了创建表格的环境：table和tabular。

示例代码：

{% highlight tex %}
\documentclass{article}

\begin{document}

\begin{table}[h!]
  \centering
  \caption{Some Table}
  \label{tab:table1}
  \begin{tabular}{l|c|r}
    1 & 2 & 3\\
    \hline
    a & b & c\\
  \end{tabular}
\end{table}

\end{document}
{% endhighlight %}

生成的pdf文档：

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 16.43.55.png)

### 代码解释：

&符做为列的分割符；\\\\做为行的分割符；\\begin\{tabular\}\{l\|c\|r\}中的'\|'代表竖线，l，c，r分别代表表格中的文本左对齐、居中对齐、右对齐；\\hline代表横线；\\caption和 \\label是标题和标签。

示例代码（带列标题）：

{% highlight tex %}
\documentclass{article}

\usepackage{booktabs}

\begin{document}

\begin{table}[h!]
  \centering
  \caption{Some Table.}
  \label{tab:table1}
  \begin{tabular}{ccc}
    \toprule
    col1 & col2 & col3\\
    \midrule
    ddd & eee & fff\\
    ggg & hhh & iii\\
    jjj & hhh & mmm\\
    \bottomrule
  \end{tabular}
\end{table}

\end{document}
{% endhighlight %}

生成的pdf文档：

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 17.22.16.png)

像上面那样手动创建表格有个缺点。如果表格较小，完全可以手写；但是当表格较大时，手动书写费时费力。你可以使用一个叫pgfplotstable的包，它可以从csv生成表格。