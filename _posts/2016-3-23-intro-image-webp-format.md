---
layout: post
title: 使用WebP图像格式
---

WebP，它的非官方发音*web屁*。它是google在5年前开发的一种图像格式，主要面向web。如果你是web设计人员或软件开发人员，并且需要优化减少图片大小，那么WebP是最好的选择。

WebP图像格式的特点总结如下：

* WebP图像文件的扩展名是 **_.webp_**
* WebP支持无损和有损压缩
* WebP无损压缩图像可以比JPEG图像格式小25-34%
* WebP有损压缩图像可以比png图像格式小25%。
* WebP支持透明度，alpha
* WebP支持动画，GIF动态图

总而言之，和JPEG，GIF，PNG格式相比，WebP可以显著的减少图像文件大小，这也是WebP非常适合应用在web上的原因（它节省了带宽，提高网页加载速度）。

下面我对几种常用图像进行了对比，实际看一下WebP的优势。

### 一个小对比实验

比较JPEG，PNG和GIF图像转换为WebP图像，文件大小对比。

随便找一个JPEG图像。原始文件大小2.2M。

![jpeg pic]({{ site.baseurl }}/images/2016/3/8fffa491jw1f2rdfughnkj21000qoth9.jpg)

使用转换工具转换，这里有几个工具：[转换WebP工具](http://blog.topspeedsnail.com/archives/4032)。

转换完成的webp图像，大小965k。

### 览器的支持

![webp 浏览器支持]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 15.48.12.png)

浏览器Chrome对webp的支持最好，毕竟是google自家的东西。FireFox和Safari还不支持webp，但是你可以使用 [WebPJS](http://webpjs.appspot.com/) JavaScript库把WebP转换为data URI。

### 判断，如果浏览器不支持webp格式，转用jpg/png格式

为了避免浏览器因为不支持webp而造成的图片加载错误，可以进行一下判断，代码如下：

{% highlight html %}
<picture>
    source srcset="example.webp 1x" type="image/webp">
    <img src="example.jpg">
</picture>
{% endhighlight %}

如果使用的是Firefox或Safari，会加载example.jpg。

> 更多资源
>
> Photoshop webp插件：[WebPFormat](http://telegraphics.com.au/sw/product/WebPFormat)
>
> WebP图像浏览器：[Mac OS X](https://github.com/emin/WebPQuickLook)，[Windows](https://developers.google.com/speed/webp/docs/webp_codec?hl=en)
>
> [webp在线转换工具](http://image.online-convert.com/convert-to-webp)