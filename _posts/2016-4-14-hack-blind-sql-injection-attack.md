---
layout: post
title: 盲SQL注入攻击
---

盲SQL注入攻击(blind SQL injection attack)是[SQL注入攻击](http://topspeedsnail.com/hack-sql-injection-attack/)的一种类型，这种攻击方式是问数据库"真假"问题，然后根据数据库的回应判断答案－应用程序输出的错误信息。

盲SQL注入和SQL注入的不同是从数据库中获得数据的方式，当数据库不向网页上输出数据时，攻击者通过问数据库一系列的"真假"问题获得敏感数据。

### 基于内容

假设有一个根据ID号显示文章的简单网页，攻击者可以执行几个简单的测试来判断这个页面是否可以执行SLQ注入攻击。

示例网页：

```
http://blogspot.com/article.php?id=10
```

发送到数据库的查询：

{% highlight sql %}
SELECT title, dateTime, content FROM article WHERE ID=10
{% endhighlight %}

攻击者注入返回"假"的SQL查询：

```
http://blogspot.com/article.php?id=10 and 1=2
```

SQL查询语句变为：

{% highlight sql %}
SELECT title, dateTime, content FROM article WHERE ID=10 and 1=2
{% endhighlight %}

如果web应用容易受到SQL注入攻击，那么它可能不会返回任何东西。为了确认，攻击者再次注入返回"真"的SQL查询：

```
http://blogspot.com/article.php?id=10 and 1=1
```

如果真假两次查询返回的数据内容不一样，攻击者就可以判断什么时候SQL语句返回ture/false。一旦把这一点确认之后，攻击者就可以根据不同SQL语句执行不同的任务。

### 基于时间

这种攻击方式依赖数据库响应时间。根据返回结果的时间长短可以判断出SQL语句是否成功执行。

以MySQL为例：

条件判断语句：

{% highlight sql %}
SELECT IF(expression, true, false)
{% endhighlight %}

如果expression表达式为真，执行一些延时操作，如，BENCHMARK()：

```
BENCHMARK(5000000，ENCODE('MSG', 'by 5 sec'))
```

执行ENCODE函数5000000次，影响了查询响应时间。

组合起来：

{% highlight sql %}
UNION SELECT IF(SUBSTRING(passwd,1,1)='a', BENCHMARK(5000000，ENCODE('MSG', 'by 5 sec')), null) FROM users WHERE id=1;
{% endhighlight %}

如果数据库响应时间变长，也许id==1的的用户密码第一个字符为'a':

使用这种方法依次探测其余的密码字符。

这个方法和上面的不同，它不影响数据库返回的数据。

很显然，上面我们使用了已知的字段名，其实，这些字段名有可能猜出来，也可以慢慢尝试（查看错误信息）。

手动执行上面的攻击是很费时的，幸运的是有很多现成的自动化工具，有一个工具叫[SQLMap](sqlmap.org):

![sqlmap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 12-24-45.png)

![sqlmap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 12-37-19.png)

[黑客常用攻击方式汇总](http://topspeedsnail.com/hacker-attack-method/)