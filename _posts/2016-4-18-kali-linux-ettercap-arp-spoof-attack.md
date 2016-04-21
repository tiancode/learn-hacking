---
layout: post
title: Kali Linux ettercap的使用
---

ettercap是执行ARP欺骗嗅探的工具，通常用它来施行中间人攻击。

我还介绍过另一个arp欺骗工具-arpspoof：

* [使用Kali Linux执行中间人攻击](http://topspeedsnail.com/kali-linux-preform-man-in-middle-attack/)

我使用的是Kali Linux 2.0；在开始使用ettercap之前，先配置一下：

编辑配置文件/etc/ettercap/etter.conf：

{% highlight shell %}
# vim /etc/ettercap/etter.conf
{% endhighlight %}

找到privs一段，改为：

```
ec_uid = 0                # nobody is the default
ec_gid = 0                # nobody is the default
```

在176行"if you use iptables"，去掉注释：

```
    redir_command_on = "iptables -t nat -A PREROUTING -i %iface -p tcp --dpor    t %port -j REDIRECT --to-port %rport"
    redir_command_off = "iptables -t nat -D PREROUTING -i %iface -p tcp --dpo    rt %port -j REDIRECT --to-port %rport"
```

保存退出。

如果你没有打开端口转发，打开方法：

* [Linux开启端口转发](http://blog.topspeedsnail.com/archives/4384)

*****

ettercap图形用户界面：Applications->Sniffing & Spoofing->ettercap-graphical：

![Kali Linux ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-18 21-57-41.png)

Options菜单里确保选择Promisc mode；

Sniff菜单中选择Unified sniffing：选择使用的网络接口，我使用wlan0；如果你使用有线，选择eth0；

![Kali Linux ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-18 22-04-44.png)

Host->Scan for hosts，扫描当前网络中的所有主机。

Host->Host list，扫描到的主机列表：

![Kali Linux ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-18 22-14-28.png)

然后我们就可以选择要攻击的目标了，例如，选择192.168.0.105的IP地址，点击Add to Target 1（添加到目标1）,然后选择网关的IP地址192.168.0.1，点击Add to Target 2（添加到目标2）。所有从192.168.0.105发送的数据都会经过Kali Linux。

如果还要截获发送给192.168.0.105的数据，把192.168.0.1添加到Target 1，192.168.0.105添加到Target 2，这实现双向监听数据。

可以添加多个主机。

查看添加的攻击目标：Targets->Current targets：

![Kali Linux ettercap]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-18 22-25-05.png)

再次确保已开启端口转发，有时会自己关上，不知道为什么：

{% highlight shell %}
# echo '1' > /proc/sys/net/ipv4/ip_forward
{% endhighlight %}

开始攻击：Mitm->ARP Poisoning，选择参数，Sniff remote connections。

这个时候目标主机的所有流量都是通过攻击者的主机出去的，想抓啥就抓啥。

和Wireshark配合使用：

* [在Wifi网络中嗅探明文密码(HTTP POST请求)](http://topspeedsnail.com/wireshark-hack-http-post-password/)

*********

ettercap命令行工具就不解释了。看man手册就成了。