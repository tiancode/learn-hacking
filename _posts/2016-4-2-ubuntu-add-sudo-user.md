---
layout: post
title: Ubuntu创建sudo用户
---

sudo命令提供了临时使用root权限的机制，使普通用户可以执行超级管理员任务。

我要在Ubuntu系统上创建一个新用户，并且有执行sudo命令的权限。

我不直接修改sudoers文件。

### 首先创建一个新用户

如果你使用已存在的用户，可以跳过这一步。

只有root用户有权限添加新用户：

{% highlight shell %}
# adduser username
{% endhighlight %}

把username替换为你的用户名。根据提示设置密码及其他信息。

现在这个用户并不能执行root任务。

### 把用户添加到sudo组

{% highlight shell %}
# usermod -aG sudo username
{% endhighlight %}

在Ubuntu上，sudo组里的成员有执行sudo的权限。

### 测试

使用su命令切换到新用户：

{% highlight shell %}
# su - username
{% endhighlight %}

执行root任务：

{% highlight shell %}
$ sudo apt-get update
{% endhighlight %}

*****

如果出现如下信息，表示这个用户不能执行sudo命令：

```
username is not in the sudoers file.  This incident will be reported.
```