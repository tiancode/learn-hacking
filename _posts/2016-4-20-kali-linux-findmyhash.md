---
layout: post
title: Kali Linux - findmyhash命令-破解哈希值
---

哈希密码就是对口令进行一次性的加密处理（哈希算法）而形成的杂乱字符串，人们认为从哈希串中是不可能还原出原口令的。

'test'使用md5哈希加密后->'098f6bcd4621d373cade4e832627b4f6'

![findmyhash]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-21 at 12.13.31.png)

所谓破解要么使用字典攻击法，要么采用穷举法，这两种方法都要靠运气。

* [Kali Linux：使用John the Ripper破解密码](http://topspeedsnail.com/John-the-Ripper-learn/)

findmyhash另辟蹊径，它借助在线破解哈希的网站，可以在极短的时间内得到密码。当然，它也不能做到100%破解。

直接执行findmyhash，查看帮助信息：

{% highlight shell %}
# findmyhash
{% endhighlight %}

![findmyhash]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-21 at 12.41.28.png)

如破解上面的MD5哈希串'098f6bcd4621d373cade4e832627b4f6'：

{% highlight shell %}
# findmyhash MD5 -h 098f6bcd4621d373cade4e832627b4f6
{% endhighlight %}

![findmyhash]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-21 09-13-40.png)

如果findmyhash破解不了，可以使用hashcat暴力破解。