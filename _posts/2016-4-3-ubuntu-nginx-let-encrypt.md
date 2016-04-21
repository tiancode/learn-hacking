---
layout: post
title: Ubuntu 16.04安装配置Nginx使用Let's Encrypt
---

Let's Encrypt是新的认证授权（CA）方式，使用它可以获得免费的TLS/SSL证书－使用HTTPS加密web server。Let's Encrypt依然在测试阶段，目前，它只支持在Apache web服务器上实现自动安装。但是，Let's Encrypt允许我们非常容易的获得一个免费的SSL证书，之后我们可以在web服务器上手动配置安装。

### 本文涉及：

* 在Ubuntu 16.04上安装Nginx
* 使用Let's Encrypt获得免费的SSL证书
* 配置Nginx使用SSL证书
* 怎么自动更新SSL证书

### 安装前提

* 你必须有一个域名
* 域名的A记录指向要配置的web服务器
* 你还要有Ubuntu 16.04的root权限

我使用test.com和www.test.com域名做示例，本文中所有涉及test.com的地方，需要替换为你的域名。

## 1）下载Let's Encrypt客户端

首先使用Let's Encrypt获得SSL证书，下载letsencrypt。

letsencrypt托管在github，使用git clone下载。

如果没有安装git，安装它：

{% highlight shell %}
$ sudo apt-get update
$ sudo apt-get install git
{% endhighlight %}

我把Let’s Encrypt clone到/opt目录：

{% highlight shell %}
$ sudo git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
{% endhighlight %}

## 2）获得SSL证书

如果你没有安装Nginx，安装它：

{% highlight shell %}
$ sudo apt-get install nginx
{% endhighlight %}

配置Nginx：

{% highlight shell %}
$ sudo vim /etc/nginx/sites-available/default
{% endhighlight %}

在server块内添加：

```
        location ~ /.well-known {
                allow all;
        }
```

/.well-known的用处：Let's Encrypt服务器要对你的web服务器进行验证，确保是你的域名，你的服务器。

你也可以更改网站根目录，默认是**/var/www/html**。

重新加载Nginx使更改生效：

{% highlight shell %}
$ sudo systemctl reload nginx
{% endhighlight %}

获得SSL证书：

{% highlight shell %}
$ cd /opt/letsencrypt
$ ./letsencrypt-auto certonly -a webroot --webroot-path=/var/www/html -d test.com -d www.test.com
{% endhighlight %}

在安装过程中提示输入邮箱，用来恢复密钥：

![letsencrypt]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 12.28.57.png)

接受协议：

![letsencrypt]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-03 at 12.30.20.png)

如果成功，会输出如下信息：

```
IMPORTANT NOTES:
...
 - Congratulations! Your certificate and chain have been saved at
   /etc/letsencrypt/live/test.com/fullchain.pem. Your
   cert will expire on 2016-06-15. To obtain a new version of the
   certificate in the future, simply run Let's Encrypt again.
...
```

注意证书保存路径和过期时间。

如果有错误，注意打开防火墙的80和443端口。

其实证书文件保存在/etc/letsencrypt/archive目录中，/etc/letsencrypt/live/test.com里的证书只是指向/etc/letsencrypt/archive最新证书的链接。获得的证书文件：

{% highlight shell %}
sudo ls -l /etc/letsencrypt/live/test.com
{% endhighlight %}

* cert.pem: 你域名的证书
* chain.pem: Let's Encrypt chain证书
* fullchain.pem: cert.pem 和 chain.pem 合并
* privkey.pem: 你的证书密钥

为了增加安全，你应该生成Diffie-Hellman：

{% highlight shell %}
$ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
{% endhighlight %}

下面你需要配置Nginx使用fullchain.pem做为证书文件，privkey.pem做为密钥。

## 3）配置Nginx使用TLS/SSL

现在已经有了SSL证书，下面来配置Nginx使用证书。

编辑Nginx配置文件/etc/nginx/sites-available/default：

{% highlight shell %}
$ sudo vim /etc/nginx/sites-available/default
{% endhighlight %}

找到server块，注释或删除掉以下行：

```
        listen 80 default_server;
        listen [::]:80 default_server;
```

在server块内添加如下配置代码使用HTTPS：

```
        listen 443 ssl;

        server_name test.com www.test.com;

        ssl_certificate /etc/letsencrypt/live/test.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/test.com/privkey.pem;
```

在server块内添加如下代码配置SSL协议：

```
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        ssl_dhparam /etc/ssl/certs/dhparam.pem;
        ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_stapling on;
        ssl_stapling_verify on;
        add_header Strict-Transport-Security max-age=15768000;
```

最后我们还需要添加一个server块，用来重定向http请求（80->443）：

```
server {
    listen 80;
    server_name test.com www.test.com;
    return 301 https://$host$request_uri;
}
```

保存退出。

重新加载Nginx使更改生效：

{% highlight shell %}
$ sudo systemctl reload nginx
{% endhighlight %}

OK，现在你的web服务器应该支持HTTPS了。

## 4）自动更新SSL证书

Let’s Encrypt证书的有效期是3个月，但是我建议你每两个月更新一下证书。

更新证书命令：

{% highlight shell %}
$ /opt/letsencrypt/letsencrypt-auto renew
{% endhighlight %}

使用cron计划任务实现自动更新证书：

{% highlight shell %}
$ sudo crontab -e
{% endhighlight %}

添加：

```
30 2 * * 1 /opt/letsencrypt/letsencrypt-auto renew >> /var/log/le-renew.log
35 2 * * 1 /bin/systemctl reload nginx
```

保存退出。

****

如果你需要更新letsencrypt客户端，简单的执行git pull：

{% highlight shell %}
$ cd /opt/letsencrypt
$ sudo git pull
{% endhighlight %}