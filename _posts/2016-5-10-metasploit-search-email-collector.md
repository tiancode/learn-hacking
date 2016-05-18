---
layout: post
title: 使用Metasploit收集邮箱信息
---

关于Metasploit的另两个帖子：

* [演示使用Metasploit入侵Windows](http://topspeedsnail.com/kali-linux-n-hack-windows-xp/)
* [演示使用Metasploit入侵Android](http://topspeedsnail.com/kali-linux-metasploit-hack-android/)

Metasploit提供了很多辅助的模块，非常实用。今天介绍一个叫search_email_collector的模块，它的功能是查找搜索引擎（google、bing、yahoo），收集和某个域名有关的邮箱地址。

### 使用步骤：

启动msfconsole：

{% highlight shell %}
# service postgresql start
# msfconsole
{% endhighlight %}

搜索模块：

```
msf > search gather auxiliary
```

找到search_email_collector：

![使用Metasploit收集邮箱信息]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-12 at 11.17.28.png)

使用search_email_collector：

```
msf > use auxiliary/gather/search_email_collector
```

![使用Metasploit收集邮箱信息]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-12 at 11.21.00.png)

注：如果你不能使用google搜素，把SEARCH_GOOGLE设置为false：

```
 > set SEARCH_GOOGLE false
```

要收集某个域名的邮箱信息：

```
> set DOMAIN your_target.com
```

开始收集：

```
> run
```

由于使用搜索引擎，所以并不保证100%可靠。

黑客可以利用这些信息进行网络钓鱼，骗取个人信息。其实这种攻击是社会工程学攻击中最不危险的一种。

类似的工具还有theharvester：

```
# theharvester
# theharvester -d microsoft.com -l 500 -b google -h myresults.html
# theharvester -d microsoft.com -b pgp
# theharvester -d microsoft -l 200 -b linkedin
# theharvester -d apple.com -b googleCSE -l 500 -s 300
```