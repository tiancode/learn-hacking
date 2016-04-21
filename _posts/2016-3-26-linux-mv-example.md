---
layout: post
title: Linux mv命令使用示例－移动或重命令文件/目录
---

mv命令和cp命令类似，但是它不复制文件/目录。这个命令默认安装在Linux系统中，不管你使用的什么发型版。下面列举了mv命令的基本使用。

### \#1) 移动文件

把 **test.jpg** 文件移动到 **~/Pictures** 目录：

{% highlight shell %}
$ mv test.jpg ~/Pictures
{% endhighlight %}

### \#2) 移动多个文件

如果你想一次移动多个文件，例如，把 **test1.jpg、test2.jpg、test3.jpg** 移动到 **~/Pictures** 目录：

{% highlight shell %}
$ mv test1.jpg test2.jpg test3.jpg ~/Pictures
{% endhighlight %}

你也可以使用模式匹配，例如，把当前目录所有jpg文件移动到 **~/Pictures** 目录：

{% highlight shell %}
$ mv *.jpg ~/Pictures
{% endhighlight %}

### \#3) 移动目录

{% highlight shell %}
$ mv dir1/ dir2/
{% endhighlight %}

把 **dir1、dir2** 移动到 **dir3** 中：

{% highlight shell %}
$ mv dir1/ dir2/ dir3/
{% endhighlight %}

### \#4) 重命名文件

mv命令也可以用来重命名文件。为了做到这一点，需要目标文件路径和源文件路径相同，并且文件名不能相同。

把 **test.jpg** 重命名为 **abc.jpg**：

{% highlight shell %}
$ mv test.jpg abc.jpg
{% endhighlight %}

如果使用绝对路径，看起看这样：

{% highlight shell %}
$ mv /home/bibi/test.jpg /home/bibi/abc.jpg
{% endhighlight %}

### \#5) 重命名目录

同上面的重命名文件类似：

{% highlight shell %}
$ mv dir1/ dir2/
{% endhighlight %}

### \#6) 查看mv的输出信息

当你移动大文件或目录时，你想知道移动是否成功，使用 **-v** 选项：

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 18.57.30.png)

### \#7) 使用交互模式

当你移动一个文件到另一个目录时，如果目标目录已经有了一个同名文件，mv默认会覆盖文件，不会有任何提示信息。我们可以使用 **-i** 选项：

~/目录中已有一个叫test1.txt的文件

{% highlight shell %}
$ mv -i test.txt ~/
{% endhighlight %}

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 19.06.37.png)

按y覆盖文件，否则不覆盖。

### \#8) 使用-U选项

如果目标文件没有要移动的文件新，那么移动文件，否则，不移动文件。

{% highlight shell %}
$ mv -uv *.txt ~/
{% endhighlight %}

### \#9) 不要覆盖任何已存在的文件

使用 -n 选项：

{% highlight shell %}
$ mv -vn *.txt ~/
{% endhighlight %}

### \#10) 当目标文件已存在，备份这个文件，然后再移动

这可以防止不小心覆盖文件，导致数据丢失。

使用 -b 选项：

{% highlight shell %}
$ mv -bv *.txt ~/
{% endhighlight %}

备份的文件以 **~** 结尾。

******

更多帮助，查看man手册：

{% highlight shell %}
$ man mv
{% endhighlight %}