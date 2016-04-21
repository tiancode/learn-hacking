---
layout: post
title: Android逆向工具：Androguard（一）
---

本文介绍一下Androguard的安装和使用。

### 什么是Androguard？

Androguard是使用Python编写的逆向工具，它可以在多个平台上运行－Linux/Windows/OSX。使用它可以反编译android应用，也可以用来做android app的静态分析（static analysis）。

### 下载安装Androguard

这里只介绍了在Linux上的安装步骤。我使用的是Kali Linux，其他Linux发行版同样适用。

确保系统中已安装了Python；一般Linux系统都自带Python。

安装IPython和pygments：

{% highlight shell %}
# pip install ipython
# pip install pygments
{% endhighlight %}

Androguard的源码托管在github，使用git clone下载源码：

{% highlight shell %}
# git clone https://github.com/androguard/androguard.git
{% endhighlight %}

安装androguard：

{% highlight shell %}
# cd androguard
# python setup.py install
{% endhighlight %}

我在使用最新源码时，遇到如下错误：

> Python.utils.traitlets.TraitError: The 'config' trait of an InteractiveShellEmbed instance must be a Config or None, but a value of class 'traitlets.config.loader.Config' (i.e. {}) was specified.

使用v2.0版本没有问题：

{% highlight shell %}
# git checkout v2.0    (最新稳定版本是v2.0)
# python setup.py install
{% endhighlight %}

### 使用Androguard反编译一个应用程序

Androguard支持3个反编译工具：

* DAD
* dex2jar + jad
* DED

下面我使用DAD反编译一个android应用：

1）运行androlyze：

{% highlight shell %}
# androlyze.py -s
{% endhighlight %}

![Androguard]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-16 17-35-41.png)

2）反编译apk文件

{% highlight python %}
a,d,dx = AnalyzeAPK("path/apk", decompiler="dad")
{% endhighlight %}

3）查看app的所有Activity

{% highlight python %}
a.get_activities()
{% endhighlight %}

![Androguard]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-16 17-44-59.png)

4）查看应用的权限

{% highlight python %}
a.get_permissions()
{% endhighlight %}

![Androguard]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-16 17-48-25.png)

5）其他方法

获得程序中所有类名：

{% highlight python %}
d.get_classes_names()
{% endhighlight %}

获得程序中定义的字符串：

{% highlight python %}
d.get_strings()
{% endhighlight %}

获得程序中定义方法：

{% highlight python %}
d.get_methods()
{% endhighlight %}

****

Androguard文档：http://doc.androguard.re/html/index.html

****

[Android逆向工具：Androguard（二）](http://topspeedsnail.com/reversing-engineering-android-androguard2/)

[移除Android应用广告－Android逆向工程](http://topspeedsnail.com/android-reversing-remove-ad/)

[Android逆向工程基本环境设置](http://topspeedsnail.com/android-reversing-env-setup/)