---
layout: post
title: 在Ubuntu上安装Android Studio
---

什么是Android Studio？

**Android Studio** 是google官方的集成开发环境（IDE），它是用来开发Android应用程序的，基于 [IntelliJ IDEA](https://www.jetbrains.com/idea/)

**在Ubuntu上安装Android Studio**

最简单的方法是使用PPA。多谢webupd8team制作的PPA。

Android Studio的需要JDK 7或JDK 8。 让我们先来安装JDK。

执行如下命令，添加PPA：

{% highlight shell %}
$ sudo add-apt-repository ppa:webupd8team/java
{% endhighlight %}

{% highlight shell %}
$ sudo apt-get update
{% endhighlight %}

安装JDK 7：

{% highlight shell %}
$ sudo apt-get install oracle-java7-installer
{% endhighlight %}

如果你要使用JDK 8，执行：

{% highlight shell %}
sudo apt-get install oracle-java8-installer
{% endhighlight %}

安装过程中需要接受协议，选择OK：

![jdk 7]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 16.06.57.png)

选择Yes：

![jdk 7]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 16.09.06.png)

等待安装完成。

安装完之后，检查JDK是否正确安装。查看Jdk版本：

{% highlight shell %}
$ java -version
{% endhighlight %}

你应该能看到java版本信息：

```
java version "1.7.0_80"
Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)
```

下面我们来安装Android Studio，添加PPA：

{% highlight shell %}
$ sudo add-apt-repository ppa:paolorotolo/android-studio
{% endhighlight %}

{% highlight shell %}
$ sudo apt-get update
{% endhighlight %}

安装Android Studio：

{% highlight shell %}
$ sudo apt-get install android-studio
{% endhighlight %}

安装完成之后，从菜单启动Android Studio（如果菜单没有，可以重启试试）。在第一次启动时，Android Studio会启动一个设置向导，引导你完成adnroid sdk、android模拟器和其他组件的下载和安装。

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 21.57.22.png)

Next：

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 21.58.24.png)

Next：

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 21.59.28.png)

Next：

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 22.00.23.png)

Finish：

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 22.01.24.png)

等待andorid sdk安装完成。

Android studio的样子：

![Android Studio]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 22.02.57.png)

现在，开始开发android app吧。