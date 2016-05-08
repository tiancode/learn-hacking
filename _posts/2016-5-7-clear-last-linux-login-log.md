---
layout: post
title: 清除Linux的最新近登录日志和Bash历史
---

前文介绍了怎么[使用tor实现匿名扫描/SSH登录](http://topspeedsnail.com/use-tor-hide-your-ass/)。本文介绍怎么清除Linux的最近登录日志和Bash历史。

### 清除登录日志

Linux系统有三个标准的显示用户最近登录信息的命令： last, lastb,和lastlog。

这些命令的输出信息包括登录用户名、最近登录时间、IP地址等。

为了更好的保持匿名，你可以清除这些信息。

```
last命令，对应的日志文件/var/log/wtmp； 成功登录用户
lastb命令，对应的日志文件/var/log/btmp； 尝试登录信息
lastlog命令，对应的日志文件/var/log/lastlog； 显示最近登录信息
```

清空日志文件：

```
# echo > /var/log/wtmp
# echo > /var/log/btmp
# echo > /var/log/lastlog
```

****

### 清除Bash历史

你可以在执行命令时，指定Bash不保存执行历史：

{% highlight shell %}
$ <空格>command
{% endhighlight %}

在要执行命令前加一个空格。

清除当前登录session的历史：

{% highlight shell %}
$ history -r
{% endhighlight %}

清除所有历史：

{% highlight shell %}
$ history -cw
{% endhighlight %}