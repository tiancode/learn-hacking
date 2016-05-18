---
layout: post
title: Ubuntu 14.04升级到Ubuntu 16.04
---

下面记录了从Ubuntu 14.04/15.10升级到Ubuntu 16.04的步骤。

在升级系统之前，我们先更新一下系统。打开终端执行如下命令：

{% highlight shell %}
$ sudo apt-get update 
$ sudo apt-get dist-upgrade
{% endhighlight %}

上面命令会下载安装最新的内核和软件包。

重启系统完成安装：

{% highlight shell %}
$ sudo reboot
{% endhighlight %}

执行如下命令打开更新管理器：

{% highlight shell %}
$ sudo update-manager -d
{% endhighlight %}

它会自动查找最新可用版本，如下图：

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 09.27.58.png)

从上图可以看到，我使用的系统版本是14.04，可以升级到版本是16.04。点击Upgrade升级。

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 09.31.55.png)

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 09.35.05.png)

等待安装完成，之后重启系统。

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 09.36.37.png)

升级到Ubuntu 16.04：

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 10.36.54.png)

**********

# 升级Ubuntu Server

前面我升级的是Ubuntu桌面版，下面我们来升级Ubuntu服务器版。

**Ubuntu 14.04/15.10 Server**升级到**Ubuntu 16.04 Server**。

如果你的系统中没有安装update-manager-core软件包，安装它：

{% highlight shell %}
$ sudo apt-get install update-manager-core
{% endhighlight %}

编辑文件_/etc/update-manager/release-upgrades_：

{% highlight shell %}
$ sudo vim /etc/update-manager/release-upgrades
{% endhighlight %}

我的server系统是Ubuntu 15.10，设置Prompt=normal：

![Ubuntu 16.04 update]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-26 at 10.17.34.png)

* Normal：检查新版本，如果有多个新版本可以升级，系统试图升级离当前使用的版本最近的。
* LTS：检查长期支持新版本，如果当前版本不为LTS，不要使用它。

如果你的系统是Ubuntu 14.04 Server，设置Prompt=lts。

在升级系统之前，我们先更新一下系统。打开终端执行如下命令：

{% highlight shell %}
$ sudo apt-get update && sudo apt-get dist-upgrade
{% endhighlight %}

重启系统：

{% highlight shell %}
$ sudo reboot
{% endhighlight %}

如果你和我一样，使用ssh登录服务器升级，建议使用screen，防止SSH连接断开。

安装screen：

{% highlight shell %}
$ sudo apt-get install screen
{% endhighlight %}

启动screen：

{% highlight shell %}
$ screen
{% endhighlight %}

升级Ubuntu：

{% highlight shell %}
$ sudo do-release-upgrade -d
{% endhighlight %}

根据提示，一路Y，Y，Y。。。

等待升级完成。