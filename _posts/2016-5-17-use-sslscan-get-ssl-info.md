---
layout: post
title: 使用sslscan获得SSL/TLS信息
---

SSLscan主要探测基于ssl的服务，如https。SSLscan是一款探测目标服务器所支持的SSL加密算法工具。

SSlscan的代码托管在[Github](https://github.com/DinoTools/sslscan)

> SSLScan queries SSL services, such as HTTPS, in order to determine the ciphers that are supported. SSLScan is designed to be easy, lean and fast. The output includes preferred ciphers of the SSL service, the certificate and is in Text and XML formats.

使用HTTPS可以防止中间人攻击，但是只有当配置正确并使用强加密才行。

关于SSL协议的漏洞也爆出了不少。

**使用示例：**

{% highlight shell %}
# sslscan your_target
{% endhighlight %}

![使用sslscan获得SSL/TLS信息]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-18 at 09.25.10.png)

Heartbleed是TLS实现上的一个漏洞，2014年4月爆出。更多信息：<https://en.wikipedia.org/wiki/Heartbleed>

![使用sslscan获得SSL/TLS信息]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-18 at 09.28.41.png)

上图显示服务器支持的加密算法，红字认为是不那么安全的加密算法，黄字中等安全。

![使用sslscan获得SSL/TLS信息]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-18 at 09.32.57.png)

SSL证书信息，RSA key的长度建议是2048 bit。

***

Kali Linux中还有一个叫SSLyze的工具，配合sslscan获得更多信息：

{% highlight shell %}
# sslyze --regular your_target
{% endhighlight %}

SSL/TLS信息也可以用OpenSSL命令获得：

{% highlight shell %}
# openssl s_client -connect your_target:443
{% endhighlight %}

****

基于sslscan的工具：TLSSLed

它是一个Linux shell脚本,它的功能是测试目标SSL/TLS(HTTPS)WEB 服务器的安全性。

{% highlight shell %}
# tlssled your_target 443
{% endhighlight %}