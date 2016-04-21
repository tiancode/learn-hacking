---
layout: post
title: 使用CSS绘制桃心
---

CSS3扩展了html和css的功能，它允许我们实现更复杂的样式。下面让我们看看，怎么使用css创建桃心形状。

![桃心]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 20.40.06.png)

桃心可以通过两个基本的形状组成，一个正方形和两个圆形，如下图：

![桃心]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 20.33.31.png)

把上图顺时针旋转45度就是一个桃心。

创建一个基本的html页面：

{% highlight html %}
<html>
  <head>
    <title>绘制桃心</title>
    <meta charset="UTF-8">
  </head>

  <style>
    .my_true_heart{
      position: fixed;
      top: 30%;
      left: 30%;
      width: 200px;
      height: 200px;
      background-color: rgba(255,15,24, 0.8);
    }
   </style>

  <body>
    <div class="my_true_heart"></div>
  </body>

</html>
{% endhighlight %}

上面代码绘制了一个正方形：

![红正方型]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 20.57.52.png)

然后在正方形的左边绘制一个圆－在同等大小的正方形上内切出一个圆：

{% highlight css %}
.my_true_heart:before{
    position: absolute;
    bottom: 0px;
    left: -100px;
    width: 200px;
    height: 200px;
    content: '';
    -webkit-border-radius: 50%;
    -moz-border-radius: 50%;
    -o-border-radius: 50%;
    border-radius: 50%;
    background-color: rgba(255,15,24, 0.8);
}
.my_true_heart:before{
    bottom: 0px;
    left: -100px;
}
{% endhighlight %}

再在上方绘制同样的一个圆：

{% highlight css %}
.my_true_heart:after{
  position: absolute;
  width: 200px;
  height: 200px;
  content: '';
  -webkit-border-radius: 50%;
  -moz-border-radius: 50%;
  -o-border-radius: 50%;
  border-radius: 50%;
  background-color: rgba(255,15,24, 0.8);
}
.my_true_heart:after{
  top: -100px;
  right: 0px;
}
{% endhighlight %}

![桃心]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 20.33.31.png)

顺时针旋转桃心45度，在my_true_heart中加入：

{% highlight css %}
-webkit-transform: rotate(45deg);
-moz-transform: rotate(45deg);
-ms-transform: rotate(45deg);
-o-transform: rotate(45deg);
transform: rotate(45deg);
{% endhighlight %}

把透明度调整为1，完整代码如下：

{% highlight html %}
<html>
  <head>
    <title>绘制桃心</title>
    <meta charset="UTF-8">
  </head>

  <style>
    .my_true_heart{
      position: fixed;
      top: 30%;
      left: 30%;
      width: 200px;
      height: 200px;
      -webkit-transform: rotate(45deg);
      -moz-transform: rotate(45deg);
      -ms-transform: rotate(45deg);
      -o-transform: rotate(45deg);
      transform: rotate(45deg);
      background-color: rgba(255,15,24, 1);
    }
    .my_true_heart:before{
      position: absolute;
      bottom: 0px;
      left: -100px;
      width: 200px;
      height: 200px;
      content: '';
      -webkit-border-radius: 50%;
      -moz-border-radius: 50%;
      -o-border-radius: 50%;
      border-radius: 50%;
      background-color: rgba(255,15,24, 1);
    }
    .my_true_heart:before{
      bottom: 0px;
      left: -100px;
    }
    .my_true_heart:after{
      position: absolute;
      width: 200px;
      height: 200px;
      content: '';
      -webkit-border-radius: 50%;
      -moz-border-radius: 50%;
      -o-border-radius: 50%;
      border-radius: 50%;
      background-color: rgba(255,15,24, 1);
    }
    .my_true_heart:after{
      top: -100px;
      right: 0px;
    }
   </style>

  <body>
    <div class="my_true_heart"></div>
  </body>

</html>
{% endhighlight %}

![桃心]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 20.40.06.png)

