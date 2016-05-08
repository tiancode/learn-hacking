---
layout: post
title: 使用fcrackzip破解zip保护密码
---

zip是一种非常流行的压缩格式，并且它提供了一个密码保护的功能 － 只有输入正确的密码才能解压。

本帖介绍一个叫fcrackzip的工具，使用它就可以破解zip密码。

![fcrackzip破解zip密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 13.41.14.png)

Kali Linux默认安装了这个工具，如果你使用的是其它Linux发行版。例如Ubuntu，执行安装命令：

{% highlight shell %}
$ sudo apt-get install fcrackzip
{% endhighlight %}

注：由于这个工具使用的是暴力破解方式，对弱密码非常有效；如果遇到强密码，这个工具恐怕无能为力。

## 创建一个测试用的zip压缩文件

{% highlight shell %}
# vim test.txt   随便写入内容，一定要写
# zip --password 12345 crack_this.zip test.txt 
{% endhighlight %}

上面命令把test.txt文件压缩为crack_this.zip，并且设置密码12345。

如果试图解压则需要输入密码：

![fcrackzip破解zip密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 13.50.17.png)

## 破解

### 使用穷举法：

{% highlight shell %}
# fcrackzip -b -c 'aA1!' -l 1-10 -u crack_this.zip 
{% endhighlight %}

-b代表brute-force；-l限制密码长度；-c指定使用的字符集：

![fcrackzip破解zip密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 13.56.05.png)

由于我知道zip的密码是数字，所以我可以执行（加快破解速度）：

{% highlight shell %}
# fcrackzip -b -c '1' -l 1-10 -u crack_this.zip 
{% endhighlight %}

![fcrackzip破解zip密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 14.03.10.png)

### 使用字典：

下面以Kali Linux自带的rockyou字典为例，你可以去网上下载GB级的大字典。

使用前先解压：

{% highlight shell %}
# gzip -d /usr/share/wordlists/rockyou.txt.gz
{% endhighlight %}

使用字典破解：

{% highlight shell %}
# fcrackzip -D -p /usr/share/wordlists/rockyou.txt -u crack_this.zip
{% endhighlight %}

![fcrackzip破解zip密码]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 14.16.53.png)

****

关于fcrackzip的更多信息请看man手册：

{% highlight shell %}
# man fcrackzip
{% endhighlight %}