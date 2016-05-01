---
layout: post
title: Kali Linux安装Flash插件
---

Kali Linux并没有自带Adobe Flash播放器插件；

在Kali Linux上有两种方法安装Flash；第一种方法比较简单，但是有时不能安装成功；

### 方法1

使用默认仓库安装：

{% highlight shell %}
# apt-get install flashplugin-nonfree
{% endhighlight %}

{% highlight shell %}
# update-flashplugin-nonfree --install
{% endhighlight %}

重启。

### 方法2

去adobe官网下载：https://get.adobe.com/flashplayer/

下载tar包：

![Kali Linux安装Flash插件]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-23 14-16-19.png)

解压下载的tar包：

{% highlight shell %}
# tar -xf install_flash_player_11_linux.x86_64.tar.gz
{% endhighlight %}

把解压出来的libflashplayer.so文件移动到火狐的插件目录：

{% highlight shell %}
# mv libflashplayer.so /usr/lib/mozilla/plugins/
{% endhighlight %}