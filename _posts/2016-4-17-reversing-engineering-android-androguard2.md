---
layout: post
title: Android逆向工具：Androguard（二）
---

在[Android逆向工具：Androguard（一）](http://topspeedsnail.com/reversing-engineering-android-androguard/)中我们安装了Androguard并且使用基本的命令反编译了apk文件。在这一部分，我将介绍更过Androguard工具：

* Androaxml
* Androsim
* Androdd
* Apkviewer
* Androguard GUI

## Androaxml

在做逆向时，AndroidManifest.xml是最重要的文件。使用Androguard中的Androaxml工具，我们可以轻易的获得这个文件。它其实是把二进制格式的XML文件转换为了人可以读的格式。

语法：

{% highlight shell %}
# androaxml.py -i <path/apk> -o <output_file> 
{% endhighlight %}

以实际app为例：

{% highlight shell %}
# androaxml.py -i test.apk -o output.xml
# vim output.xml
{% endhighlight %}

![androaxml]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 18-35-43.png)

## Androsim － 比较两个apk的相似度

可以用来比较原始的apk和修改后的apk。

在使用Androsim之前，需要安装几个依赖包：

* [sparsehash](https://github.com/sparsehash/sparsehash)  （Linux configure make 标准源码安装方式）
* [muparser](https://github.com/beltoforion/muparser)     （看Install.txt）
* [snappy](https://github.com/google/snappy)               (./autogen.sh configure make 标准源码安装方式)
* [bzip2](http://bzip.org)
* [zlib](http://zlib.net)

比较两个apk文件：

{% highlight shell %}
# androsim.py -i test.apk test.apk -c ZLIB -n
{% endhighlight %}

![Androsim]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 19-29-33.png)

上面是两个相同的apk文件；你可以和移除广告后的apk做对比：[移除Android应用广告－Android逆向工程](http://topspeedsnail.com/android-reversing-remove-ad/)

* -c：指定压缩的类型 (BZ2, ZLIB, SNAPPY, LZMA, XZ)
* -d：显示方法

## Androdd

导出apk文件中所有class文件中的方法。

安装依赖包：

* [pydot](https://github.com/erocarrera/pydot)

{% highlight shell %}
# androdd.py -i <path/apk> -o <output/dir>
{% endhighlight %}

![Androdd]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 20-08-49.png)

![Androdd]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 20-23-18.png)

图形输出为.ag文件，如果要输出png格式使用-f选项：

{% highlight shell %}
# androdd.py -i <path/apk> -o <output/dir> -f png
{% endhighlight %}

## Apkviewer

GraphML是XML格式，用来显示图例和节点：http://www.openthefile.net/extension/graphml

下载[yED](http://www.yworks.com/en/downloads.html#yEd)或[Gephi](https://gephi.github.io/users/download/)查看ApkViewer生成的GraphML。

安装依赖包：

* [NetworkX](http://networkx.github.io)   (pip install networkx)

{% highlight shell %}
# apkviewer -i <path/apk> -o <output/dir>
{% endhighlight %}

## androgui

一个GUI工具。

依赖包：

* PySide    (pip install pyside)-需要qt

{% highlight shell %}
# androgui.py
{% endhighlight %}

![androgui]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 21-53-00.png)

*****

[Android逆向工程基本环境设置](http://topspeedsnail.com/android-reversing-env-setup/)