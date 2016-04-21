---
layout: post
title: 暴力攻击法
---

暴力攻击法(brute force attack)是黑客常用的破解方法。通常用提前定义好的值，使用程序来猜密码；也可以像服务器发送这些值，然后分析回应结果。为了效率考虑，黑客一般使用字典。

[使用macbook破解WPA/WPA2 wifi密码](http://topspeedsnail.com/macbook-crack-wifi-with-wpa-wpa2/)

暴力攻击法通常用来破解密码和发现web应用的隐藏内容或网页。攻击者通常使用GET和POST请求，看一看我的apache访问日志：

![apache log]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-14 at 09.48.14.png)

[wordpress：禁用／关闭XML-RPC](http://blog.topspeedsnail.com/archives/2277)

### 示例1

DirBuster是用Java写的多线程程序，用来暴力列举网站的目录和文件，它也能找到隐藏的网页：

![dirbuster]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 10-14-33.png)

类似的工具还有dirb：

![dirb]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-14 10-20-44.png)

### 示例2

暴力破解网站的用户密码：[使用WPScan破解wordpress站点密码](http://blog.topspeedsnail.com/archives/4228)

[使用Hydra通过ssh破解密码](http://topspeedsnail.com/kydra-crack-ssh-and-avoid-attack/)

****

[黑客常用攻击方式汇总](http://topspeedsnail.com/hacker-attack-method/)