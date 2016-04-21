---
layout: post
title: Ubuntu 16.04安装Java JDK
---

Java JDK有两个版本，一个开源版本Openjdk，还有一个oracle官方版本jdk。下面记录在Ubuntu 16.04上安装Java JDK的步骤。

### 安装openjdk

更新软件包列表：

{% highlight shell %}
$ sudo apt-get update
{% endhighlight %}

安装openjdk-8-jdk：

{% highlight shell %}
$ sudo apt-get install openjdk-8-jdk
{% endhighlight %}

查看java版本：

{% highlight shell %}
$ java -version
{% endhighlight %}

![java Ubuntu 16.04]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 18.47.24.png)

### 安装oracle Java JDK

首先，安装依赖包：

{% highlight shell %}
$ sudo apt-get install python-software-properties
{% endhighlight %}

添加仓库源：

{% highlight shell %}
$ sudo add-apt-repository ppa:webupd8team/java
{% endhighlight %}

更新软件包列表：

{% highlight shell %}
$ sudo apt-get update
{% endhighlight %}

安装java JDK：

{% highlight shell %}
$ sudo apt-get install oracle-java8-installer
{% endhighlight %}

安装过程中需要接受协议：

![java Ubuntu 16.04]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 18.52.11.png)

查看java版本：

{% highlight shell %}
$ java -version
{% endhighlight %}

![java Ubuntu 16.04]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 20.50.46.png)

*****

如果你同时安装了以上两个版本，你可以自由的在这两个版本之间切换。执行：

{% highlight shell %}
$ sudo update-alternatives --config java
{% endhighlight %}

![java Ubuntu 16.04]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 20.54.50.png)

前面带星号的是当前正在使用的java版本，键入编号选择使用哪个版本。

编辑/etc/profile，在文件尾添加java环境变量：

{% highlight shell %}
$ sudo vim /etc/profile
{% endhighlight %}

```
＃ 如果使用oracle java
export JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/bin"

# 如果使用openjdk
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre/bin"
```

OK，在Ubuntu 16.04上安装java完成。