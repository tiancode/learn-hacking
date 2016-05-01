---
layout: post
title: Kali Linux使用crunch生成密码字典
---

crunch是生成密码字典的工具，通常用在暴力破解中。

> Crunch can create a wordlist based on criteria you specify.  The output from crunch can be sent to the screen, file, or to another program.

# 几个例子

### 生成4个数字组合的密码字典：

{% highlight shell %}
# crunch 4 4 0123456789 -o ~/wordlist.txt
{% endhighlight %}

第一个4代表生成的字符串最短几个字符，第二个4代表生成的字符串最长几个字符。

### 生成4个字母和1980组合的密码字典：

{% highlight shell %}
# crunch 8 8 abcdefghiABCDE -t @@@@1980 -o ~/wordlist.txt
{% endhighlight %}

字符集必须按小写，大写，数字，符号的顺序，使用\做为转译字符。

### 生成4个小写字母4个数字组合的密码字典：

{% highlight shell %}
# crunch 8 8 -t @@@@%%%% -o ~/wordlist.txt
{% endhighlight %}

更多信息，查看crunch的man手册，写的非常详细：

{% highlight shell %}
# man crunch
{% endhighlight %}