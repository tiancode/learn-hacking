---
layout: post
title: Kali Linux－arachni - 扫描网站漏洞
---

arachni是web应用漏洞扫描工具。

如果系统中没有安装arachni；安装arachni：

{% highlight shell %}
# apt-get install arachni
{% endhighlight %}

{% highlight shell %}
# arachni --help
{% endhighlight %}

![arachni]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-18 09-34-38.png)

arachni的项目地址：https://github.com/Arachni/arachni。

更多命令行选项：https://github.com/Arachni/arachni/wiki/Command-line-user-interface

扫描网站漏洞：

{% highlight shell %}
# arachni http://topspeedsnail.com
{% endhighlight %}

![arachni]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-18 at 09.37.56.png)

arachni也提供了web接口：https://github.com/Arachni/arachni-ui-web

*****

[Wordpress：使用WPScan检测易受攻击的插件和主题](http://blog.topspeedsnail.com/archives/2267)

[使用WPScan破解wordpress站点密码](http://blog.topspeedsnail.com/archives/4228)