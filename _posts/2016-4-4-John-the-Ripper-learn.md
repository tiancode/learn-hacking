---
layout: post
title: Kali Linux：使用John the Ripper破解密码
---

> John the Ripper免费的开源软件，是一个快速的密码破解工具，用于在已知密文的情况下尝试破解出明文的破解密码软件，支持目前大多数的加密算法，如DES、MD4、MD5等。它支持多种不同类型的系统架构，包括Unix、Linux、Windows、DOS模式、BeOS和OpenVMS，主要目的是破解不够牢固的Unix/Linux系统密码。

John the Ripper支持字典破解方式和暴力破解方式。

下面，我以破解Linux用户密码为例进行简单说明。

破解Linux用户密码需要使用到两个文件（包含用户的信息和密码hash值）：

```
/etc/passwd
/etc/shadow
```

## 创建一个测试用户-我们就来破解这个用户密码

添加一个用户test，并把密码设置为password。

创建新用户test：

{% highlight shell %}
# useradd -m test -G sudo -s /bin/bash
{% endhighlight %}

设置test的密码：

{% highlight shell %}
# passwd test
{% endhighlight %}

![Kali Linux]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-04 at 15.46.23.png)

## 使用unshadow命令组合/etc/passwd和/etc/shadow

{% highlight shell %}
# cd 
# unshadow /etc/passwd /etc/shadow > test_passwd
{% endhighlight %}

你可以对比一下test_passwd和/etc/passwd、/etc/shadow文件，其实就是一种简单的组合。

## 使用John the Ripper破解Linux用户密码

我们还需要一个字典，John带了一个小小的字典，位于/usr/share/john/password.lst。当然，你可以使用自己的字典，或上网下载TB级的字典文件。

我使用自带的字典为例，破解命令：

{% highlight shell %}
# john --wordlist=/usr/share/john/password.lst test_passwd
{% endhighlight %}

![Kali Linux]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-04 at 16.04.19.png)

从上图可以看到，john破解了test用户的密码。其实test_passwd文件中还有一个root用户，因为密码不在字典中，所以没有被破解。

查看破解信息：

{% highlight shell %}
john --show test_passwd
{% endhighlight %}

![Kali Linux]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-04 at 16.09.35.png)

***

上面是关于John the Ripper最简单的使用。更多高级用法，像暴力破解，增量模式等等，请看文档：

> <http://www.openwall.com/john/doc/MODES.shtml>