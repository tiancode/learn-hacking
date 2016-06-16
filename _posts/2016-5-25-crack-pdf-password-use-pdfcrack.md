---
layout: post
title: 使用pdfcrack破解PDF密码(Linux)
---

pdfcrack是破解PDF保护密码的Linux命令行工具。

### 安装pdfcrack

Debian系列：

{% highlight shell %}
# apt install pdfcrack
{% endhighlight %}

![破解PDF密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-26 at 09.09.08.png)

### 暴力破解

{% highlight shell %}
# pdfcrack -f filename.pdf -n 6 -m 8 -c 0123456789
{% endhighlight %}

暴力破解密码是漫长单调的过程。

上面使用的参数解释：

* -n：密码最短多少个字符
* -m：密码最长多少个字符
* -c：使用的字符集

更多选项，查看帮助：

{% highlight shell %}
# man pdfcrack
{% endhighlight %}

你可以随时使用 Ctrl+c 终止破解，它会保存破解的进度，下次继续在终止的地方执行。

![破解PDF密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-26 at 09.25.11.png)

### 使用密码字典

{% highlight shell %}
# pdfcrack -f high.pdf -w wordlist.txt
{% endhighlight %}

![破解PDF密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-26 at 09.30.58.png)