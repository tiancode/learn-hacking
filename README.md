# learn-hacking

> 渗透测试与网络安全学习笔记。下面提供的信息并非鼓励攻击，而是协助开发者测试自己的系统和网络，请勿用于非授权场景。

```
May the brute force be with you.
```

共收录 81 篇笔记。所有文章位于 [`posts/`](posts) 目录。

## 目录

- [密码破解](#密码破解)
- [无线攻击](#无线攻击)
- [嗅探 & 欺骗](#嗅探--欺骗)
- [漏洞利用与 Metasploit](#漏洞利用与-metasploit)
- [注入攻击](#注入攻击)
- [Web 应用分析](#web-应用分析)
- [信息收集](#信息收集)
- [匿名与取证](#匿名与取证)
- [社会工程学与免杀](#社会工程学与免杀)
- [Android 逆向工程](#android-逆向工程)
- [安全基础](#安全基础)
- [系统与环境搭建](#系统与环境搭建)
- [LaTeX 教程](#latex-教程)
- [其它](#其它)
- [HackThisSite 题解](#hackthissite-题解)
- [推荐资源](#推荐资源)

## 密码破解

* [使用Hydra通过ssh破解密码](posts/2016-4-16-kydra-crack-ssh-and-avoid-attack.md)
* [Kali Linux：使用John the Ripper破解密码](posts/2016-4-4-John-the-Ripper-learn.md)
* [使用Kali Linux重置Windows密码-chntpw](posts/2016-4-14-hack-windows-passwd.md)
* [Kali Linux使用acccheck破解Windows用户密码(SMB协议)](posts/2016-4-19-kali-linux-acccheck-crack-windows-passwd-smb.md)
* [使用fcrackzip破解zip保护密码](posts/2016-5-6-fcrackzip-crack-zip-password.md)
* [使用pdfcrack破解PDF密码(Linux)](posts/2016-5-25-crack-pdf-password-use-pdfcrack.md)
* [使用Metasploit破解Tomcat密码](posts/2016-5-14-crack-tomcat-password-use-metasploit.md)
* [Kali Linux使用crunch生成密码字典](posts/2016-4-23-kali-linux-crunch-generation-wordlist.md)
* [判断hash值的加密类型](posts/2016-5-12-identifier-hash-type.md)
* [Kali Linux - findmyhash命令-破解哈希值](posts/2016-4-20-kali-linux-findmyhash.md)
* [暴力攻击法](posts/2016-4-14-hack-brute-force.md)

## 无线攻击

* [Kali Linux使用Aircrack破解wifi密码(wpa/wpa2)](posts/2016-4-21-kali-linux-crack-wifi-wpa.md)
* [Kali Linux破解wifi密码(WEP)](posts/2016-4-22-kali-linux-crack-wifi-password-wep.md)
* [使用Reaver破解开启了WPS功能的wifi密码(wpa/wpa2)](posts/2016-4-22-kali-linux-crack-wifi-password-wps.md)
* [使用macbook破解WPA/WPA2 wifi密码](posts/2016-4-5-macbook-crack-wifi-with-wpa-wpa2.md)
* [创建假的wifi热点](posts/2016-5-24-fake-wifi-access-point-and-capture-all-data.md)
* [山寨wifi接入点](posts/2016-5-9-kali-linux-evil-twin-access-point.md)

## 嗅探 & 欺骗

* [在Wifi网络中嗅探明文密码(HTTP POST请求、POP等)](posts/2016-4-18-wireshark-hack-http-post-password.md)
* [使用Kali Linux执行中间人攻击(演示)](posts/2016-4-18-kali-linux-preform-man-in-middle-attack.md)
* [演示DNS欺骗攻击](posts/2016-5-18-DNS-spoofing-attack.md)
* [Kali Linux ettercap的使用](posts/2016-4-18-kali-linux-ettercap-arp-spoof-attack.md)

## 漏洞利用与 Metasploit

* [Metasploit的基本使用](posts/2016-4-15-kali-linux-metasploit-base-use.md)
* [演示使用Metasploit入侵Windows](posts/2016-4-15-kali-linux-n-hack-windows-xp.md)
* [演示使用Metasploit入侵Android](posts/2016-4-18-kali-linux-metasploit-hack-android.md)
* [黑技能测试：攻破VulnOS 2](posts/2016-5-23-hack-vulnos-for-test-your-skill.md)
* [安装使用lynis扫描Linux的安全漏洞](posts/2016-3-22-How-to-use-lynis-on-linux.md)

## 注入攻击

* [SQL注入攻击](posts/2016-4-13-hack-sql-injection-attack.md)
* [盲SQL注入攻击](posts/2016-4-14-hack-blind-sql-injection-attack.md)
* [使用sqlmap执行SQL注入攻击](posts/2016-5-8-sqlmap-injection-learn.md)
* [代码注入攻击](posts/2016-4-13-hack-code-injection-attack.md)
* [命令注入攻击](posts/2016-4-13-hack-command-injection-attack.md)

## Web 应用分析

* [使用w3af扫描网站漏洞](posts/2016-5-16-use-w3af-scan-website-vulnerability.md)
* [使用Nikto扫描网站漏洞](posts/2016-5-15-use-nikto-scan-vulnerabilities.md)
* [Kali Linux－arachni - 扫描网站漏洞](posts/2016-4-18-kali-linux-arachni.md)
* [使用hping3/nping施行DoS攻击](posts/2016-5-11-user-nping-hping3-dos.md)
* [SlowHTTPTest-慢速DoS攻击](posts/2016-5-28-SlowHTTPTest-dos-attack.md)
* [HTTrack - 克隆任意网站](posts/2016-5-1-httrack-clone-website.md)

## 信息收集

* [Kali Linux：使用nmap扫描主机](posts/2016-4-6-kali-linux-npm-scan.md)
* [arp-scan 发现本地网络中的隐藏设备](posts/2016-5-2-arp-scan-find-network-devices.md)
* [使用sslscan获得SSL/TLS信息](posts/2016-5-17-use-sslscan-get-ssl-info.md)
* [使用Metasploit收集邮箱信息](posts/2016-5-10-metasploit-search-email-collector.md)

## 匿名与取证

* [使用tor实现匿名扫描/SSH登录](posts/2016-5-2-use-tor-hide-your-ass.md)
* [清除Linux的最近登录日志和Bash历史](posts/2016-5-7-clear-last-linux-login-log.md)
* [Steghide - 隐藏秘密信息](posts/2016-4-30-steghide-hide-secret-message.md)
* [使用foremost恢复删除的文件](posts/2016-5-9-foremost-recover-del-file.md)

## 社会工程学与免杀

* [群发邮件 (setoolkit)](posts/2016-5-13-send-mess-email-setoolkit.md)
* [关于杀毒软件](posts/2016-5-18-antivirus-software-working.md)

## Android 逆向工程

* [学习Android逆向工程](posts/2016-4-9-start-learn-android-reversing.md)
* [Android逆向工程基本环境设置](posts/2016-4-11-android-reversing-env-setup.md)
* [移除Android应用广告－Android逆向工程](posts/2016-4-12-android-reversing-remove-ad.md)
* [Android逆向工具：Androguard（一）](posts/2016-4-16-reversing-engineering-android-androguard.md)
* [Android逆向工具：Androguard（二）](posts/2016-4-17-reversing-engineering-android-androguard2.md)
* [Android逆向工具(三)](posts/2016-4-17-reversing-engineering-android-other.md)

## 安全基础

* [黑客常用攻击方式汇总](posts/2016-4-8-hacker-attack-method.md)
* [安装BlackArch Linux](posts/2016-5-3-BlackArch-linux-penetration-testing.md)

## 系统与环境搭建

* [Linux上最危险的8个命令](posts/2016-3-22-Linux-most-dangerous-cmd.md)
* [Linux mv命令使用示例－移动或重命令文件/目录](posts/2016-3-26-linux-mv-example.md)
* [怎么设置Linux密码策略](posts/2016-3-25-linux-password-limit-lengh-and-complex.md)
* [Ubuntu创建sudo用户](posts/2016-4-2-ubuntu-add-sudo-user.md)
* [Ubuntu 16.04安装Java JDK](posts/2016-4-3-ubuntu16-install-java-jdk.md)
* [在Ubuntu上安装Android Studio](posts/2016-3-25-ubuntu-install-android-studio.md)
* [Ubuntu 14.04升级到Ubuntu 16.04](posts/2016-3-26-upgrade-to-ubuntu-16_04-LTS.md)
* [Linux：源码安装nodejs](posts/2016-3-23-nodejs-intro-newbe.md)
* [Ubuntu 16.04安装配置Nginx使用Let's Encrypt](posts/2016-4-3-ubuntu-nginx-let-encrypt.md)
* [CentOS 7：使用HAProxy实现Nginx负载均衡](posts/2016-4-10-centos-nginx-haproxy.md)
* [Kali Linux安装SSH Server](posts/2016-4-16-kali-linux-enable-ssh-server.md)
* [Kali Linux安装Flash插件](posts/2016-4-23-kali-linux-install-adobe-flash.md)

## LaTeX 教程

* [LaTeX简要教程1:安装texlive](posts/2016-3-27-a-learn-LaTeX-install-.md)
* [LaTeX简要教程2:第一个基于LaTeX的文档](posts/2016-3-27-b-first-latex-doc.md)
* [LaTeX简要教程3:添加段落和章节](posts/2016-3-27-c-latex-doc-section-part.md)
* [LaTeX简要教程4:包(package)－添加更多功能](posts/2016-3-27-d-latex-package-intro.md)
* [LaTeX简要教程5:数学公式排版](posts/2016-3-28-e-latex-math-formlar.md)
* [LaTeX简要教程6:添加图像/图片](posts/2016-3-30-f-latex-add-picture.md)
* [LaTeX简要教程7:生成目录](posts/2016-3-30-g-latex-content-table.md)
* [LaTeX简要教程8:添加表格](posts/2016-3-30-h-latex-add-bibliography.md)
* [LaTeX:使用circuitikz绘制电路图](posts/2016-4-1-latex-circuitikz-circuit.md)

## 其它

* [markdown基本语法](posts/2016-3-22-markdown-basic.md)
* [pep8：Python代码风格检查工具](posts/2016-3-22-python-code-style-guide.md)
* [使用WebP图像格式](posts/2016-3-23-intro-image-webp-format.md)
* [使用CSS绘制桃心](posts/2016-3-23-use-css-make-heart.md)
* [11个最流行的静态(博客)网站生成工具](posts/2016-3-24-static-website-generators_or_tools.md)

## HackThisSite 题解

如果你不知道 HackThisSite 是什么，看 [Wikipedia](https://en.wikipedia.org/wiki/HackThisSite)。

* [Basic missions](hackthissite/Basic.md)
* [Realistic missions](hackthissite/Realistic.md)
* [Application missions](hackthissite/Application.md)
* [Programming missions](hackthissite/Programming.md)
* [Phonephreaking missions](hackthissite/Phonephreaking.md)
* [Javascript missions](hackthissite/Javascript.md)
* [Forensic missions](hackthissite/Forensic.md)
* [Extbasic missions](hackthissite/Extbasic.md)
* [Stego missions](hackthissite/Stego.md)
* [Irc missions](hackthissite/Irc.md)

## 推荐资源

### GitHub 项目

* [Pastejacking](https://github.com/dxa4481/Pastejacking) - 粘贴劫持
* [PHP-backdoors](https://github.com/bartblaze/PHP-backdoors)
* [awesome-hacking](https://github.com/carpedm20/awesome-hacking)
* [metasploit-framework](https://github.com/rapid7/metasploit-framework)
* [reverse-engineering-for-beginners](https://github.com/veficos/reverse-engineering-for-beginners)
* [droidReverse](https://github.com/Juude/droidReverse)
* [RE-for-beginners](https://github.com/dennis714/RE-for-beginners)
* [warberry](https://github.com/secgroundzero/warberry)
* [security-guide-for-developers](https://github.com/FallibleInc/security-guide-for-developers)
* [Pompem](https://github.com/rfunix/Pompem) - 漏洞搜索工具
* [kali-anonsurf](https://github.com/Und3rf10w/kali-anonsurf) - Kali Linux 匿名工具
* [duckhunt](https://github.com/pmsosa/duckhunt) - 防御 RubberDucky 等键盘注入攻击
* [VolatilityBot](https://github.com/mkorman90/VolatilityBot) - 恶意样本/内存转储自动分析

### YouTube 视频

* [Kali Linux Tutorials](https://www.youtube.com/user/kalinuxx) - Kali Linux 教程频道
* [Kali Linux - Complete Training Program from Scratch](https://www.youtube.com/watch?v=fB3DI48MNno&list=PLnjNR4-S-EVqfJWovxEJyb7I0IOkKkoYM)
* [How to hack any Android Device (Kali Linux 2.0)](https://www.youtube.com/watch?v=hDsdpbAWrKA)
* [How to hack wifi 2016 (Kali Linux)](https://www.youtube.com/watch?v=Fynh7oP9Lio)
* [Kali Linux on Raspberry Pi 3](https://www.youtube.com/watch?v=6xXnUGR_e4E)

