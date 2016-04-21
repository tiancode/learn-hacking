---
layout: post
title: markdown基本语法
---

最近我在git pages上使用jekyll搭建了一个博客，就是本博客。写博客需要使用markdown，为了方便查询，我把常使用的markdown语法汇总在这里。

# 块引用(Blockquotes)

markdown：在每一行开头使用大于号

```
> ## 块引用标题
>
> 这是一个块引用文本。
>
> 这个块引用的第二段文本。
```

markdown渲染效果：

> ## 块引用标题
>
> 这是一个块引用文本。
>
> 这个块引用的第二段文本。

它对应的html代码：

{% highlight html %}
<blockquote>
    <h2>块引用标题</h2>

    <p>这是一个块引用文本。</p>

    <p>这个块引用的第二段文本</p>

</blockquote>
{% endhighlight %}

# 斜体字

斜体字起到突出强调的作用，markdown：使用一个星号或下划线包围要强调的文字

```
这是 *斜体* _字_。
```

markdown渲染效果：

这是 *斜体* _字_。

它对应的html代码：

{% highlight html %}
<p>这是 <em>斜体</em> <em>字</em>。</p>
{% endhighlight %}

# 粗体字

粗体字和斜体字一样，都起到强调突出的作用，markdown：使用两个星号或下划线包围要强调的文字

```
这是 **粗体** __字__。
```

markdown渲染效果：

这是 **粗体** __字__。

它对应的html代码：

{% highlight html %}
<p>这是 <strong>粗体</strong> <strong>字</strong>。</p>
{% endhighlight %}

# 又粗又斜

组合斜体字和粗体字，markdown：**_或*__包围

```
这是 **_粗体斜体_** __*字*__。
```

markdown渲染效果：

这是 **_粗体斜体_** __*字*__。

它对应的html代码：

{% highlight html %}
<p>这是 <strong><em>粗体斜体</em></strong> <strong><em>字</em></strong>。</p>
{% endhighlight %}

# 指定代码块

为了指定代码块，把代码块的每一行缩进一个制表符或4个空格。markdown：

```
    这是代码块第一行
    这是代码块第二行
```

markdown渲染效果：

    这是代码块第一行
    这是代码块第二行

它对应的html代码：
    
{% highlight html %}
<div class="highlighter-rouge"><pre class="highlight"><code>这是代码块第一行
这是代码块第二行
</code></pre>
</div>
{% endhighlight %}

嵌入代码可以使用单个\`: \`rm -rf /\`

# 代码块高亮

markdown：下面使用Python语言，使用其他语言，需要替换python（shell、c、cpp等等）

    ```python
    import os
    print(Hello world)
    ```

markdown渲染效果：

```python
import os
print(Hello world)
```

它对应的html代码：
{% highlight html %}
<div class="highlighter-rouge"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">os</span>
<span class="k">print</span><span class="p">(</span><span class="n">Hello</span> <span class="n">world</span><span class="p">)</span>
</code></pre>
</div>
{% endhighlight %}

# 标题

标题使用#，有几个#就是几级标题，HTML最多支持6级标题。markdown：

```
# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题
```

markdown渲染效果：

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

它对应的html代码：

{% highlight html %}
<h1 id="section-7">一级标题</h1>
<h2 id="section-8">二级标题</h2>
<h3 id="section-9">三级标题</h3>
<h4 id="section-10">四级标题</h4>
<h5 id="section-11">五级标题</h5>
<h6 id="section-12">六级标题</h6>
{% endhighlight %}

# 水平线

使用至少3个*或-表示水平线，markdown：

```
* * *

***

*****

- - -

---------------------------------------
```

markdown渲染效果：

* * *

***

*****

- - -

---------------------------------------

它对应的html代码：
{% highlight html %}
<hr />
<hr />
<hr />
<hr />
<hr />
{% endhighlight %}

# 图像

markdown：

```
![alt 描述](http://i4.hexunimg.cn/2016-02-06/182211953.jpg "标题")
```

markdown渲染效果：

![alt 描述](http://i4.hexunimg.cn/2016-02-06/182211953.jpg "标题")

它对应的html代码：

{% highlight html %}
<p><img src="http://i4.hexunimg.cn/2016-02-06/182211953.jpg" alt="alt 描述" title="标题" /></p>
{% endhighlight %}

# 强制换行

markdown：把下面`\s`替换为空格

```
在这一行后跟两个空格\s\s
下一行
```

markdown渲染效果：

在这一行后跟两个空格  
下一行

它对应的html代码：

{% highlight html %}
<p>在这一行后跟两个空格<br />
下一行</p>
{% endhighlight %}

# 链接

markdown：

```
这是一个链接 [github](http://github.com)。
```

markdown渲染效果：

这是一个链接 [github](http://github.com)。

它对应的html代码：

{% highlight html %}
<p>这是一个链接 <a href="http://github.com">github</a>。</p>
{% endhighlight %}

# 带标题的链接

markdown：

```
这是一个带标题的链接 [github](http://github.com "标题")。
```

markdown渲染效果：

这是一个带标题的链接 [github](http://github.com "标题")。

它对应的html代码：

{% highlight html %}
<p>这是一个带标题的链接 <a href="http://github.com" title="标题">github</a>。</p>
{% endhighlight %}

# 使用引用链接

你可以使用命令在引用已经定义的链接。

markdown：

```
这个markdown的基本介绍 [Markdown][1].

[1]: http://en.wikipedia.org/wiki/Markdown        "Markdown"

这个markdown的基本介绍 [Markdown][1].
```

markdown渲染效果：

这个markdown的基本介绍 [Markdown][1].

[1]: http://en.wikipedia.org/wiki/Markdown        "Markdown"

这个markdown的基本介绍 [Markdown][1].

它对应的html代码：

{% highlight html %}
<p>这个markdown的基本介绍 <a href="http://en.wikipedia.org/wiki/Markdown" title="Markdown">Markdown</a>.</p>

<p>这个markdown的基本介绍 <a href="http://en.wikipedia.org/wiki/Markdown" title="Markdown">Markdown</a>.</p>
{% endhighlight %}

# 无序列表

使用+、-或*创建无序列表。markdown：

```
+ 一
- 二
* 三
```

markdown渲染效果：

+ 一
- 二
* 三

它对应的html代码：

{% highlight html %}
<ul>
  <li>一</li>
  <li>二</li>
  <li>三</li>
</ul>
{% endhighlight %}

# 子列表

缩进四个空格，markdown：

```
+ 一
+ 二
    － 21
+ 三
    - 31
    - 32
```

markdown渲染效果：

+ 一
+ 二
    - 21
+ 三
    - 31
    - 32

它对应的html代码：

{% highlight html %}
<ul>
  <li>一</li>
  <li>二
    <ul>
      <li>21</li>
    </ul>
  </li>
  <li>三
    <ul>
      <li>31</li>
      <li>32</li>
    </ul>
  </li>
</ul>
{% endhighlight %}

# 有序列表

markdown：

```
1. 一
2. 二
3. 三
```

markdown渲染效果：

1. 一
2. 二
3. 三

它对应的html代码：

{% highlight html %}
<ol>
  <li>一</li>
  <li>二</li>
  <li>三</li>
</ol>
{% endhighlight %}

***********

上面列出的这些markdown，写blog基本够用了。如果有新的需要，我还会补充。

写这个blog时，正好听到关于<布鲁塞尔机场爆炸>的新闻，哎。