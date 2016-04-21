---
layout: post
title: 怎么设置Linux密码策略
---

这篇文章介绍怎么限制密码使用的长度、复杂度，过期时间。目的是防止用户使用弱密码，强制用户设置强密码。

Linux的用户密码是一大安全因素。如果你使用弱密码，极有可能会被人暴力破解。很多系统的安全问题都是由于使用弱密码引起的。

做为系统管理员，你应使用复杂的强密码。

[使用Hydra通过ssh破解密码](http://topspeedsnail.com/kydra-crack-ssh-and-avoid-attack/)

# 设置密码长度

默认安装下，所有基于Linux操作系统，要求用户密码至少使用6个字符。我建议密码至少不少于8位。一个强密码还需要混合大小写字母、数字和特殊字符。

## 基于Debian的系统（Debian Ubuntu Linux Mint）

基于Debian的系统一般把密码验证相关的配置文件放在/etc/pam.d/。

设置最少密码长度限制：至少8个字符。编辑 **_/etc/pam.d/common-password_** 文件：

{% highlight shell %}
$ sudo vim /etc/pam.d/common-password
{% endhighlight %}

找到如下一行：

```
password        [success=1 default=ignore]      pam_unix.so obscure sha512
```

![common password]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 10.16.00.png)

在上一行后添加 **minlen=8**，这里我设置密码长度至少8个字符。

```
password        [success=1 default=ignore]      pam_unix.so obscure sha512 minlen=8
```

保存退出。OK，现在用户不能设置少于8个字符的密码。

测试：

![test password]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 10.22.21.png)

如果提供的密码不足8位，密码将设置失败。提示信息：_You must choose a longer password_（你可以试试自定义提示信息）。

## 基于RHEL的系统（RHEL CentOS Scientific）

### RHEL7,CentOS7,Scientific7

执行如下命令设置密码长度，我设置8位：

{% highlight shell %}
# authconfig --passminlen=8 --update
{% endhighlight %}

查看最少密码位数：

{% highlight shell %}
# grep "^minlen" /etc/security/pwquality.conf
{% endhighlight %}

输入如下：

```
minlen = 8
```

### RHEL6,CentOS6,Scientific6

编辑 **/etc/pam.d/system-auth** 文件：

{% highlight shell %}
# vim /etc/pam.d/system-auth
{% endhighlight %}

修改一行如下，添加minlen=8：

```
password requisite pam_cracklib.so try_first_pass retry=3 type= minlen=8
```

# 设置密码复杂度

强制用户密码使用更多的字符集－大写字母、小写字母、数字和特殊字符。

## 基于Debian的系统（Debian Ubuntu Linux Mint）

首先安装密码复杂度检查工具库 **libpam-pwquality**：

{% highlight shell %}
$ sudo apt-get install libpam-pwquality
{% endhighlight %}

编辑 **/etc/pam.d/common-password** 文件：

{% highlight shell %}
$ sudo vim /etc/pam.d/common-password
{% endhighlight %}

安装完上面的库，这个配置文件自动添加了一行：

```
password        requisite                       pam_pwquality.so retry=3
```

我们需要使用pam_pwquality来设置密码复杂度。

![pam_pwquality]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 10.49.38.png)

如果你要求密码至少需要有一个大写字母，在上面一行后添加 **ucredit=-1**：

```
password        requisite                       pam_pwquality.so retry=3 ucredit=-1
```

要求密码至少需要有一个小写字母：

```
password        requisite                       pam_pwquality.so retry=3 lcredit=-1
```

要求密码至少需要有一个数字：

```
password        requisite                       pam_pwquality.so retry=3 dcredit=-1
```

要求密码至少需要一个除字母数字以外的其他字符：

```
password        requisite                       pam_pwquality.so retry=3 ocredit=-1
```

你也可以设置密码最少包含的字符集（minclass）：

```
password        requisite                       pam_pwquality.so retry=3 minclass=2
```

你可以自由组合：

```
password        requisite                       pam_pwquality.so retry=3 dcredit=-1 ucredit=-1 lcredit=-1 ocredit=-1
```

## 基于RHEL的系统（RHEL CentOS Scientific）

### RHEL7,CentOS7,Scientific7

设置密码中至少包含一个小写字符，执行命令：

{% highlight shell %}
# authconfig --enablereqlower --update
{% endhighlight %}

查看设置：

{% highlight shell %}
# grep "^lcredit" /etc/security/pwquality.conf
{% endhighlight %}

设置密码中至少包含一个大写字符，执行命令：

{% highlight shell %}
# authconfig --enablerequpper --update
{% endhighlight %}

查看设置：

{% highlight shell %}
# grep "^ucredit" /etc/security/pwquality.conf
{% endhighlight %}

设置密码中至少包含一个数字字符，执行命令：

{% highlight shell %}
# authconfig --enablereqdigit --update
{% endhighlight %}

查看设置：

{% highlight shell %}
# grep "^dcredit" /etc/security/pwquality.conf
{% endhighlight %}

设置密码中至少包含一个特殊字符，执行命令：

{% highlight shell %}
# authconfig --enablereqother --update
{% endhighlight %}

查看设置：

{% highlight shell %}
# grep "^ocredit" /etc/security/pwquality.conf
{% endhighlight %}

### RHEL6,CentOS6,Scientific6

编辑 **/etc/pam.d/system-auth** 文件：

{% highlight shell %}
# vim /etc/pam.d/system-auth
{% endhighlight %}

找到如下一行，修改：

```
password requisite pam_cracklib.so try_first_pass retry=3 type= minlen=8 dcredit=-1 ucredit=-1 lcredit=-1 ocredit=-1
```

上面配置了密码至少8个字符长，并且分别包含大小写字母、数字和特殊字符。

# 设置密码过期时间

我们设置如下策略：

* 一个密码使用的最长天数
* 更改密码最少天数间隔，为了不让用户频繁更改密码
* 在密码过期前多少天提醒用户

## 基于Debian的系统（Debian Ubuntu Linux Mint）

编辑文件 **login.defs**：

{% highlight shell %}
$ sudo vim /etc/login.defs
{% endhighlight %}

分别设置如下参数：

```
PASS_MAX_DAYS 100
PASS_MIN_DAYS 0
PASS_WARN_AGE 7
```

![password过期]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 11.24.32.png)

上面的例子，强制用户每100天更改一次密码，提前7天提醒用户。

注意，上面的配置只对系统中的新建用户生效。如果你要指定某个以存在的用户可以使用如下命令：

{% highlight shell %}
$ sudo chage -M <days> <username>
$ sudo chage -m <days> <username>
$ sudo chage -W <days> <username>
{% endhighlight %}

使用 **chage -l username** 命令显示用户密码信息，例：

![password]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 11.34.11.png)

你会发现Password inactive和Account expires并没有生效，执行如下命令：

{% highlight shell %}
$ sudo chage -E 24/09/2016 -m 0 -M 90 -I 10 -W 7 bibi
{% endhighlight %}

![password]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-25 at 11.40.38.png)

用户在密码过期10天后锁定。

## 基于RHEL的系统（RHEL CentOS Scientific）

和Debian系统一样。

# 防止用户再次使用以前使用过的密码

一般来说，不建议用户再次使用同一个密码。

## 基于Debian的系统（Debian Ubuntu Linux Mint）

编辑 **/etc/pam.d/common-password**：

{% highlight shell %}
$ sudo vim /etc/pam.d/common-password
{% endhighlight %}

在下面一行后添加 **remember=10**：

```
password        [success=1 default=ignore]      pam_unix.so obscure use_authtok try_first_pass sha512 remember=10
```

上面设置了不允许再次使用最近的10个密码。

## 基于RHEL的系统（RHEL CentOS Scientific）

编辑 **/etc/pam.d/system-auth**：

{% highlight shell %}
# vim /etc/pam.d/system-auth
{% endhighlight %}

在下面一行后添加 **remember=10**：

```
password     sufficient     pam_unix.so sha512 shadow nullok try_first_pass use_authtok remember=10
```

The End~