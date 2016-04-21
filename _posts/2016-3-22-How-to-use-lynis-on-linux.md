---
layout: post
title: 安装使用lynis扫描Linux的安全漏洞
---

**Lynis**是Linux平台上的一款安全漏洞扫描工具。它可以扫描系统的安全漏洞、收集系统信息、安装的软件信息、配置问题、没有设置密码的用户和防火墙等等。

Lynis是流行可靠的安全扫描工具。

前不久，Lynis更新了版本，Lynis发布了2.2.0。在这个版本上增加了新的特性和一些小的功能提升。我建议使用Lynis的最新版本2.2.0。

下面我在Ubuntu上安装Lynis 2.2.0。

### 安装Lynis

Lynis可以安装在系统中的任意目录，创建一个目录`/opt/lynis`：

{% highlight shell %}
$ sudo mkdir /opt/lynis
{% endhighlight %}

使用wget下载Lynis：

{% highlight shell %}
$ cd /opt/lynis
$ sudo wget https://cisofy.com/files/lynis-2.2.0.tar.gz
{% endhighlight %}

解压下载的tar包：

{% highlight shell %}
$ sudo tar -xvf lynis-2.2.0.tar.gz
{% endhighlight %}

### 使用Lynis

运行lynis需要root权限，执行：

{% highlight shell %}
$ cd lynis
$ sudo ./lynis
{% endhighlight %}

不给指定参数，它会列出可用的参数，如下图：

![lynis]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-22 at 10.31.44.png)

为了执行Lynis，你可以指定`--check-all`开始扫描整个Linux系统。命令如下：

{% highlight shell %}
$ sudo ./lynis --check-all
{% endhighlight %}

键入回车开始扫描系统：

![lynis scan]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-22 at 10.45.38.png)

![lynis scan]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-22 at 10.48.18.png)

执行上面命令总需要输入回车才能往下执行，你可以使用-c和-Q选项跳过用户输入：

{% highlight shell %}
$ sudo ./lynis -c -Q
{% endhighlight %}

### 创建Lynis计划任务－cron job

如果你想为你的系统创建一个日扫描报告，你可以设置cron：

{% highlight shell %}
$ crontab -e
{% endhighlight %}

添加cron任务：

{% highlight shell %}
30	22	*	*	*	root    /opt/lynis -c -Q --auditor "automated" --cronjob
{% endhighlight %}

上面任务每天晚上10:30会执行扫描，并把输出的信息保存到`/var/log/lynis.log`日志文件中。