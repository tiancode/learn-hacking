---
layout: post
title: Linux：源码安装nodejs
---

[Node.js](http://en.wikipedia.org/wiki/Nodejs)是服务端的JavaScript。这个东西最近很流行。如果你有JavaScript语言基础，并且厌倦了前端开发，你可以学习使用Nodejs开发服务器后端程序。假设你有JavaScript编程基础。

![jpeg pic]({{ site.baseurl }}/images/2016/3/node-js.jpg)

**JavaScript是怎么在服务端运行的呢？**

Node.js运行在Chrome v8环境上，v8是JavaScript引擎，可以运行JavaScript代码。

**安装Node.js**

Node的开发环境：建议使用Linux。我使用的系统为Ubuntu，下面我从源码安装Node。

安装基本开发环境：

{% highlight shell %}
$ sudo apt-get install build-essential
{% endhighlight %}

使用git clone nodejs源码：

{% highlight shell %}
$ cd
$ git clone https://github.com/nodejs/node
{% endhighlight %}

checkout最新分支，我安装时，最新版本是v4.4.1：

{% highlight shell %}
$ cd node
$ git checkout v4.4.1
{% endhighlight %}

创建一个nodejs安装目录：

{% highlight shell %}
$ mkdir ~/my_local
{% endhighlight %}

编译配置nodejs：

{% highlight shell %}
$ ./configure --prefix=$HOME/my_local/node
{% endhighlight %}

编译nodejs：

{% highlight shell %}
$ make
{% endhighlight %}

安装nodejs：

{% highlight shell %}
$ make install
{% endhighlight %}

配置环境变量：

{% highlight shell %}
echo 'export PATH=$HOME/my_local/node/bin:$PATH' >> ~/.profile
echo 'export NODE_PATH=$HOME/my_local/node:$HOME/my_local/node/lib/node_modules' >> ~/.profile
source ~/.profile
{% endhighlight %}

**测试nodejs**

使用经典的 **Hello World** 检测Nodejs是否成功安装。创建一个文件 _hello.js_，内容如下：

{% highlight javascript %}
console.log("Hello World!")
{% endhighlight %}

`console.log` 语句相当于python中的print。执行结果：

![nodejs]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-23 at 19.30.18.png)