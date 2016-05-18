---
layout: post
title: 群发邮件 (setoolkit)
---

首先，准备一个要发送的邮箱文件（一行一个邮箱地址）。

有很多收集邮箱的工具：

* [使用Metasploit收集邮箱信息](http://topspeedsnail.com/metasploit-search-email-collector/)

示例文件 email.txt：

```
test1@gmail.com
test2@163.com
test3@qq.com
```

启动Social Engineering Toolkit：

{% highlight shell %}
# setoolkit
{% endhighlight %}

![群发邮件 (setoolkit)]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-14 at 14.40.42.png)

选择1，然后选择5：

![群发邮件 (setoolkit)]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-14 at 14.44.48.png)

选择2，群发。添入email.txt文件路径：

![群发邮件 (setoolkit)]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-14 at 14.57.05.png)

你现在有两个选择，一个使用gmail发送，一个是使用自己的邮件服务器发送。

我使用gmail发送，选择1。

填入你的gmail邮箱地址、密码等等信息。然后按照提示输入邮件主题内容等等。

![群发邮件 (setoolkit)]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-14 at 15.06.02.png)