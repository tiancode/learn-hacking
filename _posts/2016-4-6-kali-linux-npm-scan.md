---
layout: post
title: Kali Linux：使用nmap扫描主机
---

nmap－Network Mapper，是著名的网络扫描和嗅探工具包。他同样支持Windows和OS X。

## 扫描开放端口和判断操作系统类型

先让我们ping一段地址范围，找到启动的主机：

{% highlight shell %}
# nmap -sP 159.203.205.0-100
{% endhighlight %}

![kail linux nmap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-05 22-24-44.png)

使用SYN扫描探测操作系统类型：

{% highlight shell %}
# nmap -sS 159.203.205.61 -O
{% endhighlight %}

扫描开放端口：

{% highlight shell %}
# nmap -sV 159.203.205.61 -A
{% endhighlight %}

## 扫描web服务器的网站目录

{% highlight shell %}
# nmap –script http-enum.nse blog.topspeedsnail.com
{% endhighlight %}

![kail linux nmap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-05 22-41-03.png)

上面使用了脚本，存放路径：(/usr/share/nmap/scripts)。目录里有各种各样的脚本。

## 扫描主机SSL Heartbleed 漏洞（2012）

{% highlight shell %}
# nmap -d –script ssl-heartbleed –script-args vulns.showall -sV 192.168.0.106
{% endhighlight %}