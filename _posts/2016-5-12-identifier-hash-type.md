---
layout: post
title: 判断hash值的加密类型
---

hash-identifier不是hash破解工具，而是用来判断hash值所使用的加密方式。

例如你要使用hashcat破解一个hash串，在破解之前你要知道知道hash串使用的加密算法。

hash-identifier支持的hash算法：

```
ADLER-32
CRC-32
CRC-32B
CRC-16
CRC-16-CCITT
DES(Unix)
FCS-16
GHash-32-3
GHash-32-5
GOST R 34.11-94
Haval-160
Haval-192 110080 ,Haval-224 114080 ,Haval-256
Lineage II C4
Domain Cached Credentials
XOR-32
MD5(Half)
MD5(Middle)
MySQL
MD5(phpBB3)
MD5(Unix)
MD5(WordPress)
MD5(APR)
Haval-128
MD2
MD4
MD5
MD5(HMAC(WordPress))
NTLM
RAdmin v2.x
RipeMD-128
SNEFRU-128
Tiger-128
MySQL
MySQL5 – SHA-1(SHA-1($pass))
MySQL 160bit – SHA-1(SHA-1($pass))
RipeMD-160
SHA-1
SHA-1(MaNGOS)
Tiger-160
Tiger-192
md5($pass.$salt) – Joomla
SHA-1(Django)
SHA-224
RipeMD-256
SNEFRU-256
md5($pass.$salt) – Joomla
SAM – (LM_hash:NT_hash)
SHA-256(Django)
RipeMD-320
SHA-384
SHA-256
SHA-384(Django)
SHA-512
Whirlpool
```

 Kali Linux默认安装了hash-identifier，如果你使用的系统没有这个工具，下载地址：<https://code.google.com/archive/p/hash-identifier/downloads>

 使用示例：

 判断hash串 098f6bcd4621d373cade4e832627b4f6 使用的加密算法。

![判断hash值的加密类型]({{ site.baseurl }}/images/2016/5/Screen Shot 2016-05-12 at 10.00.11.png)

上面的hash串最有可能使用的MD5算法。没错，上面的hash串就是使用 md5sum 生成的。

注意：这个工具并不能100%判断正确。