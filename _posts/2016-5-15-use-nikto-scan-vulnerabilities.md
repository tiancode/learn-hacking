---
layout: post
title: 使用Nikto扫描网站漏洞
---

Nikto是一个扫描Web服务漏洞的一个工具，也是使用最广泛的扫描工具之一。

[Nikto](https://cirt.net/Nikto2)在它网站上的描述：

> Nikto is an Open Source (GPL) web server scanner which performs comprehensive tests against web servers for multiple items, including over 6700 potentially dangerous files/programs, checks for outdated versions of over 1250 servers, and version specific problems on over 270 servers. It also checks for server configuration items such as the presence of multiple index files, HTTP server options, and will attempt to identify installed web servers and software. Scan items and plugins are frequently updated and can be automatically updated.

**扫描的内容包括：**

* 服务器错误配置
* 默认文件和程序
* 不安全的文件和程序
* 过期程序

**使用示例：**

{% highlight shell %}
# nikto -h http://your_target.com -o result.html
{% endhighlight %}

![使用Nikto扫描网站漏洞]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-17 at 15.51.32.png)

-h参数指定要扫描的主机；-o指定把扫描结果保存到result.html文件中，输出格式也可以是CSV、TXT和XML。

它将会用不少时间扫描，扫描完成之后查看result.html文件：

![使用Nikto扫描网站漏洞]({{ site.baseurl }}/images/2016/5/Screenshot from 2016-05-17 15-54-07.png)

****

**更多常用选项：**

* -config：使用自定义的配置文件扫描
* -update：升级插件数据库
* -Format：输出结果文件类型，它可以是CSV、HTML、NBE、SQL、TXT、XML。CSV和XML通常可以做为其他工具的输入
* -evasion：指定使用一些加密技术，避免被防火墙或其他防卫系统检测到
* -list-plugins：列出可用的插件
* -Plugins：指定使用的插件，默认使用所有插件
* -port：如果Web服务器没有使用标准的端口（80 443），你可能需要用到这个选项

**更多信息查看man：**

{% highlight shell %}
# man nikto
{% endhighlight %}