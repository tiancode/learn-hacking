---
layout: post
title: 在Wifi网络中嗅探明文密码(HTTP POST请求、POP等)
---

全世界，现在大约50%的网站没有使用SSL加密，天朝尤其多。

我们都知道通过HTTP发送的数据都是明文，没有使用任何加密，即使是在数据敏感的登录页面。

本文的目的是：如果你在不熟悉的网络环境中，要注意提高警惕。

没有人希望自己的密码暴露给他人，so，不要嗅探（狗）他人的密码。

> 想象有一个攻击者坐在某个咖啡馆里，桌子上放着他的笔记本电脑并连着咖啡馆的免费wifi。这个家伙就可以非常容易的获得网络里通信信息。如果密码是明文，连破解都省了。

系统要求：

* Wireshark
* ARP欺骗攻击(ARP spoof attack)
* 无线网卡

*******

无线网卡监听模式和混杂模式有什么不同：

* 监听模式允许网卡不用连接wifi就可以抓取特性频道的数据，就是在空气中抓取某个波段的数据。可以用在[破解wifi密码](http://topspeedsnail.com/macbook-crack-wifi-with-wpa-wpa2/)上
* 混杂模式（连接wifi）就是接收所有经过网卡的数据包，包括不是发给本机的包，即不验证MAC地址
* 普通模式下网卡只接收发给本机的包

现在的无线路由器都是和主机直接通信，如果你直接使用嗅探工具，只会得到广播信息和自己的连接信息。为了得到网络中所有设备发送的的数据，攻击者必须想办法充当网关的角色，ARP欺骗攻击就干了这样一件事。如果有路由器控制权的话就省事了。

集线器可以直接嗅探，因为所有数据的发送形式是广播。看看这：[集线器、交换机和路由器有什么不同](http://blog.topspeedsnail.com/archives/4391)。

ARP欺骗攻击(ARP spoof attack)：

* [使用Kali Linux执行中间人攻击](http://topspeedsnail.com/kali-linux-preform-man-in-middle-attack/)
* [Kali Linux ettercap的使用](http://topspeedsnail.com/kali-linux-ettercap-arp-spoof-attack/)

***

## 下载安装Wireshark

它也支持Windows、Mac OSX；下载地址：<https://www.wireshark.org/download.html>

Kali Linux自带了这个工具。

![Wireshark]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-18 at 18.25.28.png)

## ARP欺骗攻击

我选择使用ettercap，如果你不知道怎么使用，看，[Kali Linux ettercap的使用](http://topspeedsnail.com/kali-linux-ettercap-arp-spoof-attack/)。

攻击同一wifi网络中的其他主机：

![ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-19 09-00-57.png)

## 使用Wireshark抓包

现在wifi网络中所有计算机发送的数据包都经过攻击者计算机，攻击者需要抓取这些数据包。

![Wireshark]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-19 09-06-38.png)

等待其他人使用明文密码。

例如，要找HTTP POST请求，过滤：

```
http.request.method == "POST"
```

![Wireshark]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-19 09-16-16.png)

查看明文密码：

![Wireshark]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-19 09-21-05.png)

ettercap也可以抓包，它直接提取了明文密码：

![ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-19 09-27-22.png)

POP抓取的是我163的邮箱账户。我手机安装了邮件客户端，如果连接网络它会定时收取邮件，在认证的过程中就把密码暴露了。

常用的其他未加密服务：FTP、Telnet等

******

总结：

* 不要使用公共网络访问HTTP、POP等不安全服务，尽量使用HTTPS类型的网站。
* 使用VPN加密连接；顺带还能翻墙。实际上也不是100%可靠，SSH服务器和目标之间还可以做手脚。
* 密码要勤换，千万不要万年不变。
* 感觉网络无安全，既要防黑、还要防朝廷。