---
layout: post
title: Android逆向工具(三)
---

本节介绍如下4个工具：

* Smali/Baksmali
* Simplify
* Androwarn
* APKAnalyser

## Smali/Baksmali

smali/baksmali是dalvik使用的dex格式的编译／反编译工具，dalvik是Android Java虚拟机的实现。

Android开发者写的Java代码最终会编译为.dex（Dalvik Executable）文件，并打包进apk文件。为了解码一个apk文件，我们需要提取.dex文件，dex是二进制格式，不可读，还需要转换为Smali语言。

.dex ----------> smali <------------- Java源码

smali项目地址：https://github.com/JesusFreke/smali

下载Smali和BakSmali jar文件：https://bitbucket.org/JesusFreke/smali/downloads

*使用baksmali反编译.dex文件*

![baksmali]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 22-52-41.png)

命令语法：

{% highlight shell %}
# baksmali -o <output> <classes.dex>
{% endhighlight %}

*使用smali把.smali文件编译回.dex*

![baksmali]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-17 23-07-13.png)

{% highlight shell %}
# smali output -o classes.dex 
{% endhighlight %}

## Simplify

开发者为了防止自己的劳动成果被别人窃取，混淆代码能有效防止被他人破解，让代码更难理解。有时，混淆还能帮助隐藏恶意代码。也就是说我们需要反混淆。

Simplify是代码反混淆工具，输入Smali文件，生成.dex文件；然后使用[Dex2Jar](https://github.com/pxb1988/dex2jar)或[JD-GUI](http://jd.benow.ca)或其他Java反编译工具提取dex文件内容。

Simplify的项目地址：https://github.com/CalebFenton/simplify，在README中有使用方法。

## Androwarn

Androwarn是使用Smali的静态分析工具，它扫描应用的字节码，然后生成报告，

> Androwarn is a tool whose main aim is to detect and warn the user about potential malicious behaviours developped by an Android application.
> 
> The detection is performed with the static analysis of the application's Dalvik bytecode, represented as Smali.
>
> This analysis leads to the generation of a report, according to a technical detail level chosen from the user.

项目地址：https://github.com/maaaaz/androwarn/

## APKAnalyser

APKAnalyser是带图形用户界面的静态代码分析工具，包括Smali和APKTool等工具。

项目地址：https://github.com/sonyxperiadev/ApkAnalyser

*******

[Android逆向工程基本环境设置](http://topspeedsnail.com/android-reversing-env-setup/)

[移除Android应用广告－Android逆向工程](http://topspeedsnail.com/android-reversing-remove-ad/)

[Android逆向工具：Androguard（一）](http://topspeedsnail.com/reversing-engineering-android-androguard/)

[Android逆向工具：Androguard（二）](http://topspeedsnail.com/reversing-engineering-android-androguard2/)