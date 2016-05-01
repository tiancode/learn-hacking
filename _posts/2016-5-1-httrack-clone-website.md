---
layout: post
title: HTTrack - 克隆任意网站
---

HTTrack可以克隆指定网站－把整个网站下载到本地。

可以用在离线浏览上，也可以用来收集信息（甚至有网站使用隐藏的密码文件）。

一些仿真度极高的伪网站（为了骗取用户密码），也是使用类似工具做的。

Kali Linux默认安装了HTTrack。

HTTrack帮助：

{% highlight shell %}
# httrack --help
{% endhighlight %}

![HTTrack]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-01 at 18.42.40.png)

使用示例：

{% highlight shell %}
# httrack http://topspeedsnail.com -O /tmp/topspeedsnail
{% endhighlight %}

上面命令克隆了本网站。