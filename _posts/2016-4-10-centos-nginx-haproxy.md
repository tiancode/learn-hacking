---
layout: post
title: CentOS 7：使用HAProxy实现Nginx负载均衡
---

HAProxy是一款功能强大、灵活好用的反向代理的开源软件，它提供了负载均衡、服务器代理的功能。HAProxy是Willy Tarreau使用C语言编写的，它支持SSL、压缩、keep-alive、自定义日志格式和header重写。

HAProxy是轻量级的负载均衡和代理服务软件，占用系统资源较少。很多大型的网站都在使用它，例如Github、StackOverflow。

下面我安装配置HAProxy做为两个Nginx服务器的负载均衡。一共需要使用3个服务器，在一台机器上安装HAProxy，另两台机器安装Nginx服务。

# HAProxy的基本概念

## 4层和7层

HAProxy可以使用两种模式运行：TCP 4层模式和HTTP 7层模式。TCP模式：HAProxy把原始TCP数据包从客户端转向到应用服务器；HTTP模式：解析http请求，然后转向到web服务器。我们将使用HTTP 7层模式。

## 负载均衡算法

HAProxy使用负载均衡算法决定把请求发送给哪个服务器，使用的算法：

### Roundrobin－轮流算法

这是最简单的负载均衡算法。对每个新连接，总是下一个后端服务器处理。如果到达最后一个后端服务器，从头开始。

### Lastconn

有最少连接的后端服务器处理新请求。当请求量较大时非常好。

### Source

根据客户端IP决定哪个后端服务器处理。如果IP1是server1处理，那么这个IP1的所有请求都由server1处理。根据IP地址的哈希值决定后端服务器。

# 系统要求

3个CentOS 7服务器：

* 处理负载均衡的HAProxy服务器：192.168.0.101
* Nginx1服务器：192.168.0.108
* Nginx2服务器：192.168.0.109

## 第一步

编辑HAProxy服务器(102.168.0.101)的/etc/hosts：

{% highlight shell %}
vim /etc/hosts
{% endhighlight %}

添加Nginx1和Nginx2的主机名：

```
192.168.0.108    nginx1.your_domain.com     nginx1
192.168.0.109    nginx2.your_domain.com     nginx2
```

保存退出。

同样，编辑两个Nginx服务器的/etc/hosts，添加：

```
192.168.0.101    loadbalancer
```

在两个Nginx服务器上都要设置。

## 第二步

在HAProxy服务器上安装HAProxy：

{% highlight shell %}
# yum update
# yum install haproxy
{% endhighlight %}

haproxy的配置文件位于/etc/haproxy/。为了防止出错，先备份原始配置文件：

{% highlight shell %}
# cd /etc/haproxy/
# mv haproxy.cfg haproxy.cfg.backup
{% endhighlight %}

编辑配置文件：

{% highlight shell %}
# vim haproxy.cfg
{% endhighlight %}

写入如下内容：

```
#---------------------------------------------------------------------
# 全局设置
#---------------------------------------------------------------------
global
    log         127.0.0.1 local2     # 日志
 
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000                
    user        haproxy             # Haproxy在haproxy用户和组下运行
    group       haproxy
    daemon
 
    # 开启 stats unix socket
    stats socket /var/lib/haproxy/stats
 
#---------------------------------------------------------------------
# 基本设置
#---------------------------------------------------------------------
defaults
    mode                    http
    log                     global
    option                  httplog
    option                  dontlognull
    option http-server-close
    option forwardfor       except 127.0.0.0/8
    option                  redispatch
    retries                 3
    timeout http-request    10s
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout http-keep-alive 10s
    timeout check           10s
    maxconn                 3000
 
#---------------------------------------------------------------------
# HAProxy Monitoring 配置
#---------------------------------------------------------------------
listen haproxy3-monitoring *:8080                # Haproxy Monitoring 的使用端口：8080
    mode http
    option forwardfor
    option httpclose
    stats enable
    stats show-legends
    stats refresh 5s
    stats uri /stats                            # HAProxy monitoring的网址
    stats realm Haproxy\ Statistics
    stats auth testuser:test1234                # 登录Monitoring的用户和密码
    stats admin if TRUE
    default_backend app-main
 
#---------------------------------------------------------------------
# FrontEnd 配置
#---------------------------------------------------------------------
frontend main
    bind *:80
    option http-server-close
    option forwardfor
    default_backend app-main
 
#---------------------------------------------------------------------
# 使用roundrobin做为负载均衡算法
#---------------------------------------------------------------------
backend app-main
    balance roundrobin                                    # 使用的负载均衡算法
    option httpchk HEAD / HTTP/1.1\r\nHost:\ localhost    # 检查nginx服务器是否连通- 200状态码
    server nginx1 192.168.0.108:80 check                  # Nginx1 
    server nginx2 192.168.0.109:80 check                  # Nginx2
```

**配置rsyslog**

我们需要使用rsyslog记录HAProxy的日志，编辑rsyslog.conf配置文件，打开UDP的514端口：

{% highlight shell %}
# vim /etc/rsyslog.conf
{% endhighlight %}

去掉如下行的注释：

```
$ModLoad imudp
$UDPServerRun 514
```

如果你想指定特定IP，可以更改如下行：

```
$UDPServerAddress 127.0.0.1
```

保存退出。

创建rsyslog配置文件：

{% highlight shell %}
# vim /etc/rsyslog.d/haproxy.conf
{% endhighlight %}

写入如下内容：

```
local2.=info     /var/log/haproxy-access.log    # 访问日志
local2.notice    /var/log/haproxy-info.log      # haproxy执行信息
```

重启rsyslog：

{% highlight shell %}
# systemctl restart rsyslog
{% endhighlight %}

启动HAProxy：

{% highlight shell %}
# systemctl start haproxy
# systemctl enable haproxy
{% endhighlight %}

## 第三步

安装配置Nginx。

Nginx1和Nginx2服务器配置方法相同。

安装epel-release：

{% highlight shell %}
# yum install epel-release
{% endhighlight %}

安装Nginx：

{% highlight shell %}
# yum install nginx
{% endhighlight %}

创建index.html测试文件，Nginx1(192.168.0.108)：

{% highlight shell %}
# cd /usr/share/nginx/html/
# echo "<h1>nginx1.your_domain.com</h1>" > index.html
{% endhighlight %}

Nginx2(192.168.0.109)：

{% highlight shell %}
# cd /usr/share/nginx/html/
# echo "<h1>nginx2.your_domain.com</h1>" > index.html
{% endhighlight %}

启动Nginx服务：

{% highlight shell %}
# systemctl enable nginx
# systemctl start nginx
{% endhighlight %}

## 测试

测试nginx1、2，使用浏览器访问：

```
192.168.0.108
192.168.0.109
```

正常访问网站：http://192.168.0.101，如果有域名，指向这个IP。

登录HAProxy web管理页面：

```
http://192.168.0.101:8080/stats
```

你应该可以看到nginx、http请求的转发信息。