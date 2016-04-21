---
layout: post
title: LaTeX:使用circuitikz绘制电路图
---

Tikz包提供了很多绘制图形的功能，但是它并不能很好的绘制电路图。我们可以使用circuitikz包解决这个问题，使用它可以轻松绘制电路图。

示例代码：

{% highlight tex %}
\documentclass{article}

\usepackage{tikz}
\usepackage{circuitikz}

\begin{document}

\begin{figure}[h!]
  \begin{center}
    \begin{circuitikz}
      \draw (0,0)
      to[V,v=$U_q$] (0,2) % 电压源
      to[short] (2,2)
      to[R=$R_1$] (2,0) % 电阻
      to[short] (0,0);
    \end{circuitikz}
    \caption{first circuit.}
  \end{center}
\end{figure}

\end{document}
{% endhighlight %}

生成的pdf文档

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 17.51.15.png)

代码解释：

{% highlight tex %}
\draw (0,0)
      to[V,v=$U_q$] (0,2)
{% endhighlight %}

坐标(0,0)做为起始点，(0,2)做为终点，绘制电压源。_V_代表电压源，_v=$U_q$_绘制标识。同理，绘制电阻器：

{% highlight tex %}
      to[short] (2,2)
      to[R=$R_1$] (2,0)
{% endhighlight %}

更多电路图元素可以看[circuitikz文档](http://texdoc.net/texmf-dist/doc/latex/circuitikz/circuitikzmanual.pdf)。

### 添加一个电感器：

{% highlight tex %}
\documentclass{article}

\usepackage{tikz}
\usepackage{circuitikz}

\begin{document}

\begin{figure}[h!]
  \begin{center}
    \begin{circuitikz}
      \draw (0,0)
      to[V,v=$U_q$] (0,2)   % 电压源
      to[short] (2,2)
      to[R=$R_1$] (2,0)    % 电阻
      to[short] (0,0);
      \draw (2,2)
      to[short] (4,2)
      to[L=$L_1$] (4,0)   % 电感
      to[short] (2,0);
     \end{circuitikz}
    \caption{first circuit.}
  \end{center}
\end{figure}

\end{document}
{% endhighlight %}

生成的pdf文档：

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.06.09.png)

### 添加一个电容器：

{% highlight tex %}
\documentclass{article}

\usepackage{tikz}
\usepackage{circuitikz}

\begin{document}

\begin{figure}[h!]
  \begin{center}
    \begin{circuitikz}
      \draw (0,0)
      to[V,v=$U_q$] (0,2) % 电压源
      to[short] (2,2)
      to[R=$R_1$] (2,0) % 电阻
      to[short] (0,0);
      \draw (2,2)
      to[short] (4,2)
      to[L=$L_1$] (4,0)  % 电感
      to[short] (2,0);
      \draw (4,2)
      to[short] (6,2)
      to[C=$C_1$] (6,0)  % 电容
      to[short] (4,0);
    \end{circuitikz}
    \caption{first circuit.}
  \end{center}
\end{figure}

\end{document}
{% endhighlight %}

生成的pdf文档：

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.10.58.png)

****

# 电路元素画法示例

### 线

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (-1,0) to[short,o-o] (1,0);
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.15.42.png)

改变连接点：

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (-1,0) to[short,*-] (1,0);
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.17.54.png)

### 地线

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (-1,0) to[short,o-o] (1,0);
  \draw (0,0) to[short] node[ground] {} (0,-1);
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.20.27.png)

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (-1,0) to[short,o-o] (1,0);
  \draw (0,0) to[short] node[ground] {GND} (0,-1);
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.21.15.png)

### 指示电流方向

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (0,0) to[R,i=$i_1$] (2,0);
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.22.59.png)

### 晶体管

{% highlight tex %}
\begin{figure}[h!]
\begin{circuitikz}
  \draw (0,0) node[npn](npn1) {}
  (npn1.base) node[anchor=east] {B}
  (npn1.collector) node[anchor=south] {C}
  (npn1.emitter) node[anchor=north] {E};
\end{circuitikz}
\end{figure}
{% endhighlight %}

![Latex]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-02 at 18.26.42.png)