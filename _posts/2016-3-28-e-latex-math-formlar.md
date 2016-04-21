---
layout: post
title: LaTeX简要教程5:数学公式排版
---

在LaTeX中有两种对数学公式排版的模式。第一种是使用$符号嵌入到的你的文本中；第二种是使用数学"环境"。下面举几个例子说明。

### 把数学公式嵌入到文本中

只要把数学公式放在两个$符号之间，例如：

{% highlight tex %}
\documentclass{article}

\begin{document}

  Power of Two is $f(x) = x^2$ balabala

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 16.40.00.png)

### 数学公式环境

使用equation环境，在这个环境中的代码都会渲染成数学公式，例：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{equation*}
  1 + 2 = 3 
\end{equation*}

\begin{equation*}
  1 = 3 - 2
\end{equation*}

% 按等号对齐；两个斜杠代表换行，第一个斜杠是转译字符；
\begin{align*}
  1 + 2 &= 3\\
  1 &= 3 - 2
\end{align*}

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 16.52.59.png)

### 分式、积分等

LaTeX可以显示任何数学符号，下面以分数和积分为例。每个命令都有特定的参数，例：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{align*}
  f(x) &= x^2\\
  g(x) &= \frac{1}{x}\\
  F(x) &= \int^a_b \frac{1}{3}x^3
\end{align*}

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 16.59.01.png)

你也可以在命令中嵌套命令，这允许你实现更复杂的公式，例：

{% highlight tex %}
\documentclass{article}

\begin{document}

  $\frac{1}{\sqrt{x}}$

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.05.36.png)

表达式越复杂越容易出错，一定要注意{}的对应。你也可以使用公式编辑器（Lyx）编写公式。

### 矩阵

LaTeX还可以显示矩阵，放在matrix环境中，例：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{align*}
\begin{matrix}
1 & 0\\
0 & 1
\end{matrix}
\end{align*}

\end{document}
{% endhighlight %}

矩阵只能在数学环境中使用。

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.18.45.png)

带 [ ] 的矩阵模式：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{align*}
\left[
\begin{matrix}
1 & 0\\
0 & 1
\end{matrix}
\right]
\end{align*}

\end{document}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.26.14.png)

其实，left和right可以用到任何公式中：

{% highlight tex %}
\documentclass{article}

\usepackage{amsmath}

\begin{document}

$\left(\frac{1}{\sqrt{x}}\right)$

\end{document}
{% endhighlight %}

生成的pdf：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.28.17.png)

*******

## 常用的LaTeX数学命令：

三角函数：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.32.28.png)

微积分：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.34.51.png)

.->\cdot；⋯->\cdots

其他：

![Latex]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-28 at 17.37.56.png)

> 完整的LATEX符号表：<http://tug.ctan.org/info/symbols/comprehensive/symbols-a4.pdf>