---
layout: post
title: 使用Kali Linux重置Windows密码-chntpw
---

首先制作一个Kali Linux启动U盘：

[使用dd命令制作USB启动盘](http://blog.topspeedsnail.com/archives/4042)

在要破解密码的电脑上插入U盘，启动Kali Linux，进入Live模式。

我安装了Windows 8.1和Kali Linux双系统，我就在Kali Linux上破解Windows密码。

打开终端命令行，导航到Windows保存密码的目录：Windows/System32/config，几乎所有的Windows版本都把密码保存在sam文件中。在Kali linux上挂载的路径为：/media/hda1/Windows/System32/config：

![sam]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 16-05-17.png)

用户的密码就保存在这里文件里。

Kali Linux上有一个叫chntpw的工具：

> change password of a user in a Windows SAM file, or invoke registry editor. Should handle both 32 and 64 bit windows and all version from NT3.x to Win8.1

使用如下命令查看Windows系统中所有的用户：

{% highlight shell %}
# chntpw -l sam
{% endhighlight %}

![sam]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 16-15-35.png)

上面命令列出了系统中的用户，假设要修改用户tian的密码：

{% highlight shell %}
# chntpw -u "tian" sam
{% endhighlight %}

![sam]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 16-19-58.png)

我们有好几个选项，你可以清空密码，提升用户权限等等。这个工具的旧版本有更改密码一项，貌似是因为在有些系统上不起作用，所有去掉了这个功能。