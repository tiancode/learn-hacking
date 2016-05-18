---
layout: post
title: SQL注入攻击
---

SQL注入攻击(SQL injection attack)是攻击者把SQL语句插入到应用程序的输入数据中，或web表单的输入域，总之就是欺骗服务器执行恶意SQL语句。

SQL注入攻击是黑客对数据库进行攻击的常用手段之一。一次成功的SQL注入，允许你读取数据库中的敏感数据、修改数据库、执行数据库的管理员操作等。

SQL注入是数据库驱动型网站所面临的普遍问题，SQL注入漏洞常见于PHP和ASP应用：

* 输入不信任的数据
* SQL语句是动态构建的

### 示例1

假设有一个SQL查询：

{% highlight sql %}
SELECT id, name, nickname FROM users
{% endhighlight %}

如果有人提供如下信息：

```
name：evil'man
nickname：test
```

查询语句应为：

{% highlight sql %}
SELECT id, name, nickname FROM users WHERE name = 'evil'man' AND nickname = test
{% endhighlight %}

执行时会报错：

```
Incorrect syntax near il' as the database tried to execute evil.
```

在构建SQL语句要小心，下面是安全的Java代码：

{% highlight java %}
String name = req.getParameter('name');
String nickname = req.getParameter('nickname');

String sqlQuery = "SELECT id, name, nickname FROM users WHERE name = ? AND nickname = ?";
PreparedStatement pstmt = connection.prepareStatement(sqlQuery);
pstmt.setString(1, name);
pstmt.setString(2, nickname);
{% endhighlight %}

### 示例2

下面是一段C#代码，它动态构造一个SQL查询语句：

{% highlight c# %}
string username = ...
string item = ...

string sqlQuery = "SELECT * FROM items WHERE username = "'" + username + "' AND itemname = '" + item + "'";
{% endhighlight %}

想要执行的查询语句如下：

```
SELECT * FROM items
WHERE username = 
AND itemname = 
```

上面的语句只有在itemname中没有单引号时正确。如果在查询语句后添加`OR 1=1`，where限制条件将失效：

```
SELECT * FROM items
WHERE username = 'usr'
AND itemname = 'item' OR 1=1
```

等同于：

```
SELECT * FROM items
```

这允许攻击者查询到权限外的数据。

sqlmap是利用这种攻击的一个自动化工具：[使用sqlmap执行SQL注入攻击](http://topspeedsnail.com/sqlmap-injection-learn/)

****

防止SQL注入攻击的方法：

* 对输入的数据进行检验，可以使用白名单／黑名单
* 使用存储过程

[黑客常用攻击方式汇总](http://topspeedsnail.com/hacker-attack-method/)