---
layout: post
title: Steghide - 隐藏秘密信息
---

> Steghide is a steganography program that is able to hide data in various kinds of image- and audio-files. The color-respectivly sample-fre‐quencies are not changed thus making the embedding resistant against first-order statistical tests.

Steghide是数据隐藏工具，通过此工具你可以轻松的将文件隐藏到一个图片/音频中。一旦文件被隐藏到图片中，那么图片看起来依然就是图片，可以正常使用图片浏览工具打开查看图片，唯一的区别是它里面包含着被隐藏的文件。这样做的好处是便于传播或发送一些私密的文件，防止被人截取。

Steghide可以把信息隐藏在AU, BMP, JPEG 或 WAV格式的文件中。

## 安装Steghide

{% highlight shell %}
# apt-get install steghide
{% endhighlight %}

## 以一个文本文件为例

创建一个文本文件，随便写入点东西：

{% highlight shell %}
# vim my_secret.txt
{% endhighlight %}

![Steghide]({{ site.baseurl }}/images/2016/4/Screen Shot 2016-04-30 at 09.31.12.png)

我要把my_secret.txt隐藏到图片中：

{% highlight shell %}
# steghide embed -ef my_secret.txt -cf normal_pic.jpg
{% endhighlight %}

设置密码；

下图中包含了隐藏文件（和原始图片相比文件变大了）：

![Steghide]({{ site.baseurl }}/images/2016/4/normal_pic.jpg)

获得隐藏文件：

{% highlight shell %}
# steghide extract –sf normal_pic.jpg
{% endhighlight %}